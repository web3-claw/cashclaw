# Changelog

## [1.1.0] - 2026-03-14

### Added
- **Mission Audit Trail** — Every mission step is now logged with timestamps. What was requested, what was delivered, and the full output trail. No invoice goes out without proof.
- `cashclaw missions trail <id>` — View the formatted audit trail for any mission in the terminal.
- `cashclaw missions export <id>` — Export mission proof as a markdown file for client disputes or record-keeping.
- `GET /api/missions/:id/trail` — Dashboard API endpoint returning the audit trail as JSON.

### Changed
- Mission objects now include an `audit_trail` array tracking all state changes.
- All mission lifecycle functions (create, start, complete, cancel, step update) log trail entries automatically.
- Dashboard health endpoint now reports version `1.1.0`.
- Updated package description to mention audit trails.

### Why This Release
Community feedback was clear: *"Without proof of actual work done, the invoice becomes negotiation."* Mission Audit Trail solves this. Every step is timestamped. Every deliverable is tracked. Dispute resolution and a work proof dashboard are on the roadmap.

## [1.0.2] - 2026-03-10

### Fixed
- CLI minor fixes and dependency updates.

## [1.0.1] - 2026-03-07

### Fixed
- Init wizard improvements and error handling.

## [1.0.0] - 2026-03-01

### Added
- Initial release with 7 built-in skills.
- Stripe payment integration.
- HYRVEai marketplace support.
- Web dashboard on port 3847.
- Mission lifecycle management.
