# Changelog

## 1.2.1

- Browse folder: one folder per family member (`Browse/Anthony/2024/03/…`), each holding only that person's photos. Existing trees are rebuilt automatically in the background the next time the copy is seen; the old year folders are cleaned up (links only — anything else left there stays). Every member's Mac needs this version: an older one keeps writing the old layout until it updates.
- The backup no longer drops to one file at a time at the end of every batch of 50.
- The window reliably opens at launch (the menu bar icon could appear before the window scene was ready).

## 1.2.0

- Several files are copied at once (Settings → Backup, default 4): on a NAS with iCloud originals, many times the throughput of 1.1.
- Fixed a stall at the start of every pass that grew with the number of files on the copy (a rename check that touched every object over the share); on a large Vault the app spent most of its time there.
- Fixed the window freezing for up to a minute when the Library count ran on a large library; the count itself went from minutes to about a second, and the catalog now uses WAL so reads and writes no longer queue behind each other.
- Close the window and Photos Vault becomes a menu bar icon with no Dock icon (Settings → General, on by default); launched at login it starts that way. "Open at login" moved to Settings → General.
- A distinct icon and message when no storage copy is connected.
- No more Keychain password dialogs: the Mac's signing key moved to a file under Application Support (migrated automatically).
- Blocking disk and share I/O runs on its own threads; the speed limit applies to the total, not per file.
- Overview: one track per file in flight, fixed in number so the card keeps its height; every step is shown (Verify and Done were too fast to see); the toolbar button no longer flashes.
- Storage Copies and Vault views use grouped sections; the Vault ID has a copy button.

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
