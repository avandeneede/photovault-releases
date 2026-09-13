# Changelog

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
