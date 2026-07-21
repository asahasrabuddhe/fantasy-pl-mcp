# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- **Live gameweek scores** (`get_gameweek_live_scores`): live player points, stats, and bonus-processing status during a gameweek
- `get_dream_team`: the official highest-scoring XI for a gameweek
- `get_manager_transfer_history`: any manager's transfers with player names and prices, grouped by gameweek
- `get_my_current_team`: authenticated current squad with purchase/selling prices, chips, and transfer state
- `suggest_captain`: ranked captain suggestions blending FPL expected points, form, points per game, and fixture difficulty
- `get_price_changes`: gameweek price risers and fallers with ownership and transfer momentum
- CI now runs lint (ruff), the full test suite on Python 3.10–3.12, and a package build on every push and pull request
- Test suite covering the HTTP layer, rate limiter, cache, concurrency helpers, all new tools, and a guard locking the registered tool/prompt/resource surface

### Fixed
- `get_league_analytics(analysis_type="decisions")` crashed with a `NameError` (undefined `limit`)
- Failed FPL logins were reported as successful (FPL returns HTTP 200 for bad credentials); the login check now verifies the session cookie
- `compare_players` returned an empty `best_performers` section when `include_gameweeks=True`
- `blank_gameweek_impact` in league fixture analysis was always empty because the data was fetched after the loop that needed it

### Changed
- HTTP layer hardened: one shared `httpx.AsyncClient` with connection pooling, request timeouts, and retry with exponential backoff on 429/5xx; public and authenticated requests share a single rate limiter
- League analytics fetches per-manager data concurrently (bounded) instead of sequentially, removing the main cause of timeouts; the team ceiling rises from 25 to 50 (configurable via `LEAGUE_RESULTS_LIMIT`)
- Cache uses diskcache's native expiry instead of hand-rolled timestamp tuples
- `__main__.py` split into per-domain tool modules; shared fixture-difficulty, gameweek, and parameter-normalization helpers extracted
- Packaging: `setup.py` removed (single-sourced from `pyproject.toml`); version defined in exactly one place; black/flake8/isort replaced by ruff
- Nickname search map updated to current players

## [0.1.6] - 2025-07-31

### Added
- Upgrade to newer package versions
- Prepare for FPL 25/26 Season

## [0.1.5] - 2025-07-31

### Added
- Encrypted credential storage for improved security
- Automatic migration from plaintext credentials

### Security
- Credentials are now encrypted at rest
- Enhanced authentication system

## [0.1.4] - 2025-03-31

### Added
- Team ID support for accessing any team's data
- FPL authentication system for private data access
- Manager information tools with profile and performance data
- Team details with player selection and captain choices
- League support for both public and private mini-leagues
- League analytics with historical performance and ownership trends
- Team historical performance tracking across gameweeks
- League fixture analysis for upcoming matches

## [0.1.3] - 2025-03-15

### Added
- Prompts for easy usage
- Minor fixes


## [0.1.2] - 2025-03-15

### Added
- Enhanced player analysis capabilities
- Position normalization utilities
- Extended player comparison with gameweek history
- Fixture analysis for players, teams, and positions
- Improved caching for better performance

## [0.1.1] - 2025-03-14

### Added
- Fixture support

### Fixed
- Duplicate code

## [0.1.0] - 2025-03-14

### Added
- Initial release
- FPL data access through MCP resources
- Player comparison tools
- Team and player search functionality
- Gameweek information resources
- Modern packaging with pyproject.toml
- Automated Claude Desktop integration