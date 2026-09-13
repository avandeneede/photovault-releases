# Changelog

## 1.1.0

- New photos, edits and deletions in Photos are picked up automatically, without rescanning.
- Problems view: failed files with the reason; retry or skip them.
- Throughput and time-left estimates on backups and scans.
- Restore back into Photos, with favourites and albums; restore to a folder never overwrites.
- Journal events are signed per Mac; forged or tampered lines are rejected.
- Vault Service can run in the background (`photosvault service install`), replacing an object needs owner/admin, request bodies are capped.
- Notifications for connected/up-to-date/disconnected copies and problems; pause on battery; copy speed limit.
- Storage copies show what they are (this Mac, external disk, network share, service), their capacity, and can be renamed or removed.
- Milestone track per file; one progress track with checkmarked steps.
- Statistics computed off the main thread; nearby-copy discovery on mount events.
- French localization; VoiceOver labels; activity filter and search.

## 1.0.1

- Updates now come from the public releases repository, so installed apps can check for and install new versions.
- Current file shows its kind (photo, video, RAW, edit data) next to its name.
- Milestone track centred on its nodes; duplicate count only among files already hashed.
- Accurate first-launch instructions for a non-notarized app.

## 1.0.0

First release.

- Streams original photos and videos from Apple Photos (including iCloud-only originals) into content-addressed, verified copies on external disks, NAS shares and Vault Services.
- Several copies of one Vault fill from each other and repair each other; absence of a copy is a state, not an error.
- Deduplication across the whole family: one file per unique original per copy.
- Browse folder by year and month on every copy; restore any selection to a folder.
- Library selection by date, kind, favourites or album with live protection counts.
- Members and ownership; Macs converge through an append-only journal on every copy.
- Vault Service over HTTPS with token roles and certificate pinning.
- Optional AES-256-GCM media encryption with a family passphrase; Touch ID app lock.
- Automatic backups while running, launch at login, menu bar status, self-updates.
