# Architecture Overview — pelis-feed

## 1) Boundaries & Ownership

| Component | Owns | Runtime |
|---|---|---|
| **CLI Ingester** (`pelis ingest`) | RSS fetching, parsing, deduplication, feed health tracking, alerting | Cron-triggered process (runs and exits) |
| **FastAPI Web App** (`pelis serve`) | Filtered view rendering, read-tracking, on-demand enrichment | Long-running local process (on-demand) |
| **Database** (MySQL/SQLite) | Persistent state for movies, feed health, read status | Shared resource |
| **Config file** (`config.yaml`) | Filtering rules, connection strings, alerting config | Shared resource (read by both processes) |

### Project Structure (Proposed)

```
pelis-feed/
├── pelis/
│   ├── __init__.py
│   ├── cli.py              # CLI entry point (Click or argparse)
│   ├── config.py           # YAML config loading + validation
│   ├── models.py           # SQLAlchemy models (shared)
│   ├── db.py               # Database session/engine setup
│   ├── ingester/
│   │   ├── __init__.py
│   │   ├── fetcher.py      # RSS fetch + parse
│   │   ├── dedup.py        # Deduplication logic
│   │   └── alerter.py      # Feed health check + SMTP alert
│   ├── enrichment/
│   │   ├── __init__.py
│   │   ├── base.py         # Abstract enrichment interface
│   │   └── omdb.py         # OMDb/TMDb/imdbapi implementation
│   └── webapp/
│       ├── __init__.py
│       ├── app.py           # FastAPI app factory
│       ├── routes.py        # Route handlers
│       ├── filters.py       # Filtering + sorting logic
│       └── templates/
│           ├── base.html    # Base layout
│           ├── index.html   # Main movie list view
│           └── partials/
│               └── movie_card.html  # HTMX partial for read-toggle
├── config.yaml             # User configuration
├── requirements.txt        # Python dependencies
└── README.md
```

## 2) Interfaces

### CLI Commands

| Command | Description | Triggers |
|---|---|---|
| `pelis ingest` | Fetch RSS, parse, deduplicate, store | Cron every ~2h |
| `pelis serve` | Start FastAPI web app | Manual (on-demand) |
| `pelis check-health` | Check feed health, send alert if needed | Cron (can run with ingest or separately) |

### Web App Routes (FastAPI)

| Method | Path | Description | Response |
|---|---|---|---|
| GET | `/` | Main movie list (filtered, grouped by year) | HTML (Jinja2) |
| POST | `/movies/{id}/read` | Mark movie as read | HTMX partial (updated card) |
| POST | `/movies/{id}/unread` | Mark movie as unread | HTMX partial (updated card) |
| POST | `/movies/{id}/enrich` | Trigger on-demand rating enrichment | HTMX partial (updated card with ratings) |
| GET | `/health` | Feed health status (last fetch, errors) | HTML snippet |

### Database Interface

- Both processes connect via SQLAlchemy engine using the same `database.url` from `config.yaml`
- CLI Ingester: writes movies, updates feed_health
- Web App: reads movies (with filters), writes is_read toggle, writes enrichment results
- Concurrency: SQLite has single-writer limitation — acceptable since ingester runs briefly every 2h and web app writes are infrequent (read-tracking, enrichment)

## 3) Security Model

- **AuthN:** None — localhost-only, single user
- **AuthZ:** None — all actions available to anyone who can reach the port
- **Network:** Web app binds to `127.0.0.1` only (not exposed to network)
- **Secrets management:** Database credentials and API keys stored in `config.yaml` (file permissions: owner-only read). Not committed to git (`.gitignore`).
- **Input sanitization:** Jinja2 auto-escaping for all rendered HTML (protects against XSS from RSS feed data)

## 4) Operational Model

### Deployment
- Local machine only — no cloud, no containers
- Install via `pip install -e .` or `pip install -r requirements.txt`
- Cron entry added manually: `0 */2 * * * /path/to/pelis ingest && /path/to/pelis check-health`

### Scaling
- Not applicable (single user, local machine)
- Database: MySQL handles concurrent reads well; SQLite is sufficient for <10k movies

### Failure Modes

| Failure | Detection | Impact | Recovery |
|---|---|---|---|
| RSS feed down | `check-health` compares last_success_at to threshold | No new movies ingested | Automatic retry next cron cycle; email alert after 24h |
| RSS format changed | Parser raises warning, logs unparseable entries | Some movies not ingested | Manual parser update required |
| Enrichment API unavailable | HTTP timeout/error caught | Movie shows without ratings | User can retry via "refresh ratings" button |
| Database unreachable (MySQL) | SQLAlchemy connection error on startup | Both processes fail to start | Check MySQL service, connection string |
| Web app crash | Process exits | UI unavailable | Restart `pelis serve` |
| Disk full (SQLite) | Write error | Ingestion fails | Free disk space |

### Backup
- MySQL: standard `mysqldump` (user's responsibility)
- SQLite: file copy of `.db` file
- Config: tracked in git (minus secrets)

## 5) Technology Stack

| Layer | Technology | Version |
|---|---|---|
| Language | Python | 3.11+ |
| Web framework | FastAPI | latest |
| Templating | Jinja2 | (bundled with FastAPI) |
| Interactivity | HTMX | latest (CDN) |
| ORM | SQLAlchemy | 2.0+ |
| DB (primary) | MySQL | 8.0+ |
| DB (fallback) | SQLite | 3.x (stdlib) |
| MySQL driver | PyMySQL | latest |
| RSS parsing | feedparser | latest |
| HTTP client | httpx or requests | latest |
| Config | PyYAML | latest |
| SMTP | smtplib | (stdlib) |
| CLI | Click | latest |
| ASGI server | Uvicorn | latest |

## 6) Constraints Compliance Matrix

| Constraint | Implementation |
|---|---|
| C-001 (Python) | Entire stack is Python |
| C-002 (MySQL primary + SQLite fallback) | SQLAlchemy with configurable connection URL |
| C-003 (Two processes) | CLI ingester (cron) + FastAPI web app (on-demand) |
| C-004 (No paid APIs) | Free-tier enrichment sources only |
| C-005 (Local SMTP) | `smtplib` with configurable SMTP host |
| C-006 (Web UI via FastAPI) | FastAPI + Jinja2 + HTMX |
| C-007 (Config file) | `config.yaml` for all configurable values |
