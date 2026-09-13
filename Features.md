# Photos Vault — Features

Photos Vault backs up the **original** photos and videos of every family member's Apple
Photos library to storage you own — external disks, a NAS, or a Mac in another house —
and keeps those copies complete, verified and in sync. Apple Photos stays your photo app;
Photos Vault is the durable archive underneath it.

## Protecting a library

- **Reads originals through PhotoKit**, never the `.photoslibrary` bundle, and never
  modifies or deletes anything in Photos. iCloud-only originals are downloaded on demand.
- **Streams**: each original is hashed and written to the destination chunk by chunk.
  Memory stays at a few MB and the Mac never needs free space for the library, only Photos'
  own transient cache for one iCloud download at a time. A 10 GB video backs up with
  13 MB of RAM.
- **Verifies before it trusts**: nothing is counted as protected until it has been
  re-read from the destination and its SHA-256 matches.
- **Choose what to protect**: everything, the most recent items, or a selection by date,
  photos/videos, favourites or album — with a live count of what is already protected.
- **Resumable**: quit, sleep, unplug — the queue is persistent and picks up where it left
  off. The file in progress simply restarts.
- **Follows Photos**: new items, edits and deletions are picked up from Photos' own change
  history, without rescanning the library. New photos and videos join the backup as they
  arrive (optional).
- **Progress you can read**: throughput, time left, and for the file in progress a
  milestone track — read, copy, verify, done.
- **Problems, not mysteries**: files that failed after several attempts are listed with the
  reason; retry or skip them. Files that are skipped stay out of the counts.

## Storage copies

- **Any folder is a copy**: an external disk, a NAS share, a folder on another Mac. Several
  copies of the same Vault are independent and interchangeable.
- **Absence is normal**: a disconnected disk or an unreachable NAS shows as *Not connected*
  with what is waiting for it — never as an error. Reconnect it and the copy catches up by
  itself. Full, read-only or damaged copies are the only ones that need attention.
- **Copies fill from each other**: with a NAS and an external disk, the disk fills from the
  NAS instead of downloading from iCloud again. Sources are chosen in order: a local copy,
  Photos if the original is cached on the Mac, a copy over the network, then iCloud.
- **Self-healing**: *Verify Integrity* re-reads a copy; a damaged file is repaired from a
  healthy copy. A damaged *source* is caught before it can spread.
- **Discovery**: copies on connected disks and shares are found automatically; file
  servers on the local network are listed with a one-click Connect.
- **Vault Service**: a Mac can serve a copy over HTTPS (`photosvault serve`, or as a
  background service with `photosvault service install`) so another household can back up
  to it — token access, roles, certificate pinning.
- **Knows what it is**: each copy shows whether it is on this Mac, an external disk, a
  network share (and on which server) or a Vault Service, with its path and free space.
  Copies can be renamed or removed (the files stay).

## Deduplication

- Every original is stored **once per copy**, whoever it belongs to and however many times
  it appears. Identity is the file's SHA-256, never its name.
- Live Photos, RAW+JPEG pairs and edits' adjustment data are each protected as their own
  original resources.

## Browsing the backup

- A `Browse/` folder on each copy shows the archive as `2024/03/IMG_1023.HEIC` — links,
  not copies, so it costs nothing. Live Photo pairs sit side by side. Files open in
  Finder, Quick Look, Preview and Photos.
- **Restore**: any Library selection can be written back to a folder as real files, from
  the fastest connected copy — existing files are never overwritten — or re-imported
  **into Photos** with its favourites and albums.

## Several family members

- Anyone points their Mac at the same copy and **joins** the Vault. The first Mac is the
  owner; others are members.
- Each photo knows its owners. The same photo in two libraries is one file with two
  owners; one person removing it from Photos never touches the other's — or the file.
- Every Mac keeps a journal of what it learnt on every copy it reaches. Macs merge each
  other's journals, so a member's photos end up on everyone's copies, even when the Macs
  are never online at the same time.
- Favourites, hidden state and album membership travel with the photo, per member, so a
  restore into Photos puts them back.

## Security

- **Transport**: HTTPS with certificate pinning to a Vault Service; tokens in the Keychain.
- **App lock**: optional Touch ID or password to open the window.
- **Signed journals**: every Mac signs what it writes (Ed25519); a line another Mac cannot
  verify is ignored. A Vault Service accepts a replacement of an existing file only from
  an owner or admin.
- **Optional media encryption**, chosen when a Vault is created: AES-256-GCM in
  authenticated chunks, key derived from a family passphrase (PBKDF2-SHA256) and kept in
  the Keychain. Copies verify by decrypting; a Vault Service stores ciphertext it cannot
  read. Unencrypted Vaults remain plain files that open anywhere.

## Living with it

- Runs automatically while the app is open, keeps going in the menu bar when the window
  is closed, and can open at login.
- The menu bar shows the state at a glance (protected · backing up · waiting for storage
  · needs attention) with a one-click pause/resume.
- Activity keeps a history of what was stored, learnt and repaired; filter it to problems
  or search it.
- Notifications when a copy is connected, up to date or disconnected, and when something
  needs you. Optional: pause on battery, limit copy speed.
- Updates install themselves from GitHub releases. Available in English and French.

## What it never does

Delete anything in Photos. Modify the Photos library. Require free space equal to the
library. Count an interrupted transfer as done. Store the same bytes twice on one copy.
Delete an object because one member removed it. Treat an unplugged disk as a failure.
