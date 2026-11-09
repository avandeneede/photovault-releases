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
- **Hidden photos** are protected like the others. They get no link in `Browse/`, which
  everyone on the share can open (Photos keeps them behind Touch ID); the Photos page lists
  them under Hidden, behind a confirmation.
- **Not protected: shared albums.** Items other people put in a shared album are not part of
  your library, and Photos lists them apart; a shared-album photo you saved to your library
  is protected like any other.
- **Progress you can read**: the Overview shows your photos on their way — iCloud → this
  Mac → each copy — with what is still only in iCloud (Photos downloads it first), what is
  ready to send, each copy's share already backed up, the download and upload speeds and
  the time left. Each file in flight shows its speed (or its iCloud download) and a
  milestone track — read, copy, verify, done. Each family member's progress and speed on
  every copy are in the Vault section.
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
- **Reconnects by itself**: a copy on a NAS share is mounted silently, with the password
  saved in the Keychain, whenever its server is on the network — no trip to Finder. If the
  NAS refuses that password, the app stops trying (so the account is never locked) and the
  copy's *Connect* button asks for it once.
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

- **Photos page**: `<member> – Photos.html` at the root of each copy shows that member's protected
  photos the way Photos does — Years, Months and All Items, Favourites, Places, Albums,
  media types (Videos, Selfies, Live Photos, Portrait, Panoramas, Slo-mo, Time-lapse,
  Bursts, Screenshots, RAW…), Hidden behind a confirmation, and *Removed from Photos*:
  what was deleted from Photos since it was backed up, still in the Vault — with a viewer
  that plays videos and Live Photos. Overview → *Browse Your Photos in the Vault* → **Open** (or
  right-click a copy → *Open Photos Page*) shows it in **Library**, served from this Mac: the list comes from the catalog, thumbnails from the previews Photos keeps on the
  Mac, and only the originals you open are read from the copy — quick even on a slow NAS.
  It is reachable from this Mac only, behind a secret address that changes at every
  launch. The page also lives on the copy, so it works with no app at all: open
  `<member> – Photos.html` from the share in Safari (slower — everything is then read
  through the share). Each Mac keeps its own user's page current. (People are not
  available: Photos does not share faces with other apps.)
- A `Browse/` folder on each copy shows the archive as `Anthony/2024/03/IMG_1023.HEIC` —
  one folder per family member with only their own photos; links, not copies, so it costs
  nothing. Live Photo pairs sit side by side. Files open in Finder, Quick Look, Preview
  and Photos.
- **Browse integrity**: the Vault view shows, per member and per copy, how many protected
  files are in their folder; *Check Browse Folder* (right-click a copy) verifies every
  link on disk, relinks what is missing and reports per member.
- **Restore**: any selection (Library → Selection) can be written back to a folder as real files, from
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

- Runs automatically. Close the window and the app becomes a menu bar icon (no Dock
  icon) that keeps backing up; open at login and it starts that way. Both are settings.
- The menu bar shows the state at a glance (protected · backing up · no copy connected
  · needs attention), and while a backup runs the share of your photos already on the
  copy, with a one-click pause/resume.
- Several files travel at once (four by default, adjustable): the wait for each iCloud
  download and each round trip to a NAS overlaps instead of adding up.
- Activity keeps a history of what was stored, learnt and repaired; filter it to problems
  or search it.
- Notifications when a copy is connected, up to date or disconnected, and when something
  needs you. Optional: pause on battery, limit copy speed.
- Updates: checked at every launch and hourly; a newer version is proposed as soon as it
  exists. Available in English and French.

## What it never does

Delete anything in Photos. Modify the Photos library. Require free space equal to the
library. Count an interrupted transfer as done. Store the same bytes twice on one copy.
Delete an object because one member removed it. Treat an unplugged disk as a failure.
