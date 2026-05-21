# Data Contracts — pelis-feed

## 1) Entities

### Movie

- **Definition:** A movie entry discovered from the YTS RSS feed, potentially with multiple quality/resolution variants
- **Owner:** CLI Ingester (creates/updates), Web App (reads, marks as read, triggers enrichment)
- **Versioning:** No formal versioning — schema changes handled via SQLAlchemy `create_all()`

### FeedHealth

- **Definition:** Tracks the operational status of the RSS feed (last success, last attempt, errors)
- **Owner:** CLI Ingester (writes), Web App (reads for display), Alerting logic (reads for threshold check)
- **Versioning:** Single-row table, no versioning needed

## 2) Schema (SQLAlchemy Models)

### Movie

```python
class Movie(Base):
    __tablename__ = "movies"

    id: int                    # PK, auto-increment
    title: str                 # NOT NULL, max 500 chars
    year: int                  # NOT NULL, 4-digit year
    genres: str                # NOT NULL, JSON array stored as text (e.g., '["Action", "Thriller"]')
    torrent_url: str           # NOT NULL, unique identifier for deduplication
    qualities: str             # JSON array (e.g., '["720p", "1080p", "2160p"]')
    imdb_rating: float | None  # 0.0–10.0, nullable (not yet enriched)
    rt_expert_rating: int | None    # 0–100, nullable
    rt_audience_rating: int | None  # 0–100, nullable
    poster_url: str | None     # nullable, URL to movie poster
    feed_entry_date: datetime  # when the RSS entry was published
    enrichment_date: datetime | None  # when ratings were last fetched, nullable
    enrichment_error: str | None     # last enrichment error message, nullable
    is_read: bool              # default False
    created_at: datetime       # auto-set on insert
    updated_at: datetime       # auto-set on insert and update
```

**Indexes:**
- `ix_movies_title_year` on (title, year) — for deduplication lookups
- `ix_movies_torrent_url` UNIQUE on torrent_url — primary deduplication key
- `ix_movies_year` on year — for year-section queries
- `ix_movies_is_read` on is_read — for filtering out read movies

### FeedHealth

```python
class FeedHealth(Base):
    __tablename__ = "feed_health"

    id: int                    # PK (always 1 — single row)
    last_success_at: datetime | None  # last successful fetch timestamp
    last_attempt_at: datetime | None  # last fetch attempt timestamp
    last_error: str | None     # error message from last failed attempt
    consecutive_failures: int  # counter, reset on success
    alert_sent_at: datetime | None  # when the last downtime alert was sent
```

## 3) Validation Rules

### Movie (on ingestion)
- **V-001:** `title` MUST NOT be empty or whitespace-only
- **V-002:** `year` MUST be a 4-digit integer between 1900 and current year + 1
- **V-003:** `genres` MUST be a valid JSON array with at least one non-empty string
- **V-004:** `torrent_url` MUST be a non-empty string (used as dedup key)
- **V-005:** `qualities` MUST be a valid JSON array

### Movie (on enrichment)
- **V-006:** `imdb_rating`, if present, MUST be between 0.0 and 10.0
- **V-007:** `rt_expert_rating`, if present, MUST be between 0 and 100
- **V-008:** `rt_audience_rating`, if present, MUST be between 0 and 100

### Deduplication Logic
- **V-009:** On insert, check for existing record with same `torrent_url`
- **V-010:** If match found, merge `qualities` arrays (union of available qualities)
- **V-011:** If no URL match but same `title` + `year`, treat as same movie — merge qualities

## 4) Compatibility Rules

- **Backward compatibility:** Not applicable (single-user, no API consumers)
- **Schema evolution:** SQLAlchemy `create_all()` adds new columns; manual `ALTER TABLE` for column changes. No formal migration framework initially.
- **Data format:** `genres` and `qualities` stored as JSON text for SQLite compatibility (both backends support JSON text parsing)

## 5) Configuration Schema (YAML)

```yaml
# config.yaml

database:
  url: "mysql+pymysql://user:pass@localhost/pelis_feed"
  # Alternative: "sqlite:///./pelis_feed.db"

feed:
  url: "https://yts.ag/rss"
  poll_interval_hours: 2

alerting:
  smtp_host: "localhost"
  smtp_port: 25
  from_address: "pelis-feed@localhost"
  to_address: "user@localhost"
  downtime_threshold_hours: 24

enrichment:
  source: "omdb"  # or "tmdb", "imdbapi"
  api_key: ""     # if required by source (free tier)
  timeout_seconds: 10

filtering:
  default:
    min_imdb: 6.0
    min_rt_expert: 60
    min_rt_audience: 50
  genres:
    action:
      min_imdb: 5.5
    romantic_comedy:
      min_imdb: 5.0
    documentary:
      min_imdb: 7.0
      min_rt_expert: 80
  older_movies:
    min_imdb: 7.5
    min_rt_expert: 75
    year_threshold: 6  # movies older than this many years from current

genre_priority:
  - action
  - romantic_comedy
  - thriller
  - sci-fi
  - drama
  - horror
  - comedy
  - documentary

webapp:
  host: "127.0.0.1"
  port: 8080
```

## 6) RSS Feed Contract (External — Not Controlled)

**Source:** `https://yts.ag/rss`
**Format:** RSS 2.0 XML

**Expected fields per `<item>`:**
- `<title>` — Movie title (may include year and quality, e.g., "Movie Name (2024) [1080p]")
- `<link>` — Torrent page URL
- `<pubDate>` — Publication date
- `<description>` — HTML blob with poster, genre, rating info (requires parsing)
- `<enclosure>` — Torrent file URL (if present)

**Parsing strategy:**
- Extract title, year, quality from `<title>` via regex
- Extract genre, IMDb rating, poster URL from `<description>` HTML
- Use `<link>` or `<enclosure>` URL as deduplication key

**Risk:** Feed format is uncontrolled and may change without notice. Parser must log warnings on unexpected format changes.
