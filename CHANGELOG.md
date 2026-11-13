# Changelog

## 1.4.20

- **A backup reaches 100 % by itself.** A file iCloud keeps not sending used to end in *Needs attention* after five attempts, and stayed there: the backup sat at 99 % until you skipped it by hand — on this Mac, 4 Live Photo videos of shared albums whose photos are in the Vault. Such a file is now set aside automatically: out of what is left to do, still listed in **Problems** (“Set aside after 5 attempts: iCloud sent nothing in 5 min…”) with *Retry* and *Show in Photos*. The 4 already waiting are set aside at launch. Only this case is: a copy that refuses a file, or a hidden photo Photos will not hand over while its album is locked, still needs you. When everything else is protected, the Overview says how many files were set aside instead of claiming every original.

## 1.4.19

- **Show in Photos.** From **Problems** (button, right-click, or double-click a row) and from the viewer in **Library**, Photos Vault opens the item in Photos — to check whether a Live Photo still plays before you retry or skip it, or simply to find a photo there. The first time, macOS asks whether Photos Vault may control Photos. It works for items of this Mac's Photos library; another member's file, or a photo deleted from Photos, has no such button. The page on the copy, opened in a browser without the app, does not show it.

## 1.4.18

- **The Photos page no longer counts more than your library.** Activity said “Photos page updated — 88,305 of 88,104 items”: the first number included the 201 photos deleted from Photos that the Vault keeps (*Removed from Photos*), the second, rightly, did not. Both now count what is still in Photos — “88,104 of 88,104”. The page's own header had the same mix-up and, seeing more items than the total, dropped “out of 88,104” altogether; it shows it again.

## 1.4.17

- **1.4.16's fix now really applies.** It only counted an iCloud download as “sent nothing” if Photos had reported no progress at all, and Photos reports some as it gives up: on this Mac, the 4 shared-album Live Photo videos went on “waiting for network” under 1.4.16. What counts now is the first 3 minutes: no byte and no progress in that time, then a “network” error, is a failed attempt. A real download shows progress within seconds and still waits for the network when it drops.

## 1.4.16

- **A file iCloud never sends ends up in Problems instead of “waiting” forever.** On this Mac, the Live Photo videos of 4 items in two shared albums (≈ 6 MB) kept coming back as “Waiting for iCloud”: each time, iCloud Shared Albums gave up after 5 minutes without sending a byte, Photos reported it as a network error, and the backup waited for a network that was there and asked again a few minutes later, without end, with the copy stuck at 99 %. An iCloud download that fails as “network” after 3 minutes without a byte or any progress now counts as a failed attempt, like any other: after five, the file is listed in **Problems** with “iCloud sent nothing in 5 min”, where you can retry or skip it. A real network problem still just waits: a request that times out fails within a minute (38 s seen here), and a download cut off halfway had already started arriving. The photos of those 4 items are in the Vault; only their motion is missing.

## 1.4.15

- **Your own photos go before shared albums' items.** The backup sent files in the order they were found, so shared albums' items found by an *Entire Library* pass went before photos of your library added later: on this Mac, 78 of your own Live Photo videos (127 MB) waited for 3,000 shared items. Each pass now sends your library's photos first, then shared albums' items, then other members' files.

## 1.4.14

- **What is left counts shared albums' items.** Photos gives no size for a shared album's item until it is downloaded, and the Overview counted each one as 0 bytes: with about 3,000 of them still to send, it showed “≈ 129 MB only here · About 4 min left” for over an hour while some 3 GB went through — and the 129 MB, this Mac's own photos queued behind them, never moved. Such a file is now counted at the average size of the stored files like it (834 KB for a shared photo, 28 MB for a video on this Mac) until its real size is known, so “only in iCloud”, the percentage and the time left are realistic.

## 1.4.13

- **Shared albums are backed up.** An *Entire Library* backup now also takes the items of the shared albums you follow whose original is not in your library — other people's photos, or yours since deleted (8,110 of 18,083 shared items on this Mac). A shared copy of one of your own photos, a reduced version of an original the Vault already has, is left out: it has the original's capture time to the millisecond, kind and proportions. On the Photos page they stay out of the library, as in Photos, and are under *Shared Albums* and in their albums.
- **A full pass once a day** for a library protected as a whole (one where *Entire Library* was run): it adds what Photos' change history does not report — new items of shared albums — or missed. A library protected through a selection is never swept whole.

## 1.4.12

- Library → Selection works while the backup runs: *Recent 200*, *Entire Library* and *Add … Items to Backup* used to wait for the backup to stop — and in automatic mode it never does, so they stayed greyed out. Items are now added alongside it, and the backup picks them up on its next batch.

## 1.4.11

- **Hidden photos can be backed up.** Reading a photo's files asked Photos without including hidden items, so even a hidden photo the scan had listed was left out. That is fixed — but Photos also locks the Hidden album by default (Photos → Settings → General → *Use Touch ID or password*), and while it is locked it hands hidden photos to no app, with no way around it: on this Mac, none of 208 hidden photos are in the Vault for that reason. Turn the lock off, then Library → Selection → *Entire Library*, to back them up. In the Vault they get no link in Browse/, which everyone on the share can open; the Photos page lists them under Hidden, behind a confirmation.
- **Photos added since the first scan are caught up.** A library scanned before change tracking existed (1.0) had no starting point, so nothing added to Photos afterwards was ever seen — 1,738 photos on this Mac. At launch, one full pass catches up (it only reads what the Vault does not know yet) and sets the starting point; from then on new photos join as they arrive.

## 1.4.10

- Photos deleted from Photos stay visible in the Vault: the Photos page used to list only what was still in Photos, so a photo you deleted — or a whole library wiped — vanished from Library although its original was safe on the copy. They now have their own collection, *Removed from Photos* (under Utilities), out of the main library, favourites, albums and places. “Out of N” still counts what is in Photos.

## 1.4.9

- Your photos in the Vault are in **Library** now, where you would look for them, instead of a window of their own: Library opens on them, and a *Photos in the Vault | Selection* switch in the toolbar leads to the tools that choose what to back up and restore. Overview → *Open* and a copy's *Open Photos Page* take you there with the latest photos. Leaving Library and coming back finds the page where you left it.

## 1.4.8

- Your photos in the Vault open in a window of Photos Vault (“Photos in the Vault”) instead of a Safari tab: same page, same speed, and its secret address no longer lands in Safari's history. The viewer's Download button saves the original into Downloads. The page on the copy still opens in any browser without the app.
- Vault: another member's Mac shows when it was last heard from — its latest line in the journal — instead of the day it joined (“seen 2 months ago” for a Mac backing up right now). This Mac says “this Mac”, and the name and the time stay on one line.

## 1.4.7

- The Photos page opens in a second: the app now serves it from this Mac instead of Safari reading it from the share. Its list comes from the catalog (half a second, instead of 13–15 s over Wi-Fi from a busy NAS), its thumbnails from the previews Photos keeps on this Mac (every item has one at once, before the copy's own thumbnails are made), and switching to Favourites, an album or a place is instant: Safari re-checked a page opened from the share on every click, 3–4 s each time. Only an original you open is read from the copy. The page is reachable from this Mac only, behind a secret address that changes at every launch. The page on the copy itself is unchanged and still works without the app.
- The Photos page's sidebar and content are two matching panels, aligned at the top: no more dark notch above the sidebar.

## 1.4.6

- The backup always starts at launch. The app waited a fixed 3 s for its first status refresh; when that refresh was slower (a large journal from another Mac being merged at the same time) the backup never started, and nothing moved until something else woke it. It now starts as soon as the first refresh can tell what to send.
- Lines from other Macs' journals are no longer rejected as forged when they were signed one second before the time they carry: versions before 1.4.0 signed the time cut to the second but stored it rounded to the millisecond (about one event in 2,000). The content and the key must still match.

## 1.4.5

- The Photos page shows its pictures in Safari: it now sits at the root of the copy (“Anthony – Photos.html”), because Safari lets a page opened from a file read only its own folder and those below it — from Browse/<member>/ it could not reach the thumbnails or the originals. The old page in Browse/<member>/ is removed.
- Thumbnails are made newest first, since the page opens on the most recent photos.

## 1.4.4

- The iCloud → Mac → copy flow is balanced: three equal steps, arrows on the icons' line, the copy shown as its percentage and size (no second progress bar), the time left centred.
- Files queued behind another iCloud download say “Waiting for iCloud” instead of “0 %”; the iCloud step counts files downloading and waiting separately.
- The Overview has a “Browse Your Photos in the Vault” card: Open shows your Photos page (years, albums, places…) in Safari straight from the copy.
- The Vault section opens at once: it no longer reads the copy's settings from the NAS on every redraw (once per member), which froze the window while the share answered.

## 1.4.3

- The Overview shows where your photos are on their way: iCloud → this Mac → each copy, with what is still only in iCloud, what is on the Mac ready to send, each copy's share already backed up (a copy can be partly done, or away and catching up later), and the download and upload speeds on the arrows.
- Only your own progress is on the Overview and in the menu bar; each member's progress on every copy, with their speed, is in the Vault section.

## 1.4.2

- iCloud downloads are visible: a file whose original is only in iCloud shows “Downloading from iCloud 45 % · 2 MB/s” while Photos fetches it (often the whole video before the first byte reaches the copy) instead of “0 bytes”; the Overview and menu bar panel show the total iCloud download speed and how much of what is left is still only in iCloud.

## 1.4.1

- Speeds you can see: each file being copied shows its own speed next to its size, “Your photos on photovault” shows what this Mac is actually sending (big videos in progress included, so it is known after half a minute instead of only once files finish) and the time left from it, and each other member's row shows their speed, measured from their journal.

## 1.4.0

- Each file in flight has its own small buffer (8 MB) and writer: Photos hands every file's data over on one queue, and a slow write to the share made right there could hold back the other files' data.
- Faster on a NAS: about 14 filesystem round trips per file instead of 35 (one open to create the partial, one listing instead of several checks at commit, manifest lines written in batches, Browse links made in the background, free space measured once a minute). Measured with 80 ms per round trip: 813 → 323 ms per file with 4 files at a time.
- The journal is exchanged every minute during a backup instead of only at the start and end of a pass (which could last days), read in chunks and merged in batches; one publisher per Mac, which ends the duplicate lines written at launch. Lines another Mac's journal had wrong are reported once per pass in Activity.
- Another member's files that no connected copy holds are set aside instead of being touched one by one on every pass.
- The Vault trusts its owner first: a new Mac's journal is only applied once the owner's Mac approves it (Vault → *Waiting for approval*, with a key fingerprint to compare). Existing Macs keep working as before. A Mac speaks only for its own user and the photos it announced.
- Fixed: about 1 event in 2,000 had a signature the other Mac rejected (rounded timestamps), and such a line could stall merging that journal.
- A copy whose encryption setting changes on the share is refused; Vault Service addresses must be https.
- The Photos page appears at once on its first build (tiles fill in as thumbnails are written) instead of after all thumbnails.
- The app is signed with the hardened runtime: other software can no longer inject code into it to borrow its Photos access.
- Progress you can read: the menu bar shows how far your photos are on the copy (“36 %”) until they all are, and the menu bar panel and Overview say “Your photos on photovault — 35,334 of 98,902 files · 100 GB of 497 GB”, the time left measured over the last minutes, and each other member's progress (sent by their own Mac). Before, one bar mixed every member's files on every copy.
- Built against macOS 27; capture warnings from the Swift 6.4 toolchain fixed.

## 1.3.0

- The NAS reconnects by itself: a copy on a network share that is not mounted is mounted silently with the password saved in the Keychain as soon as its server is on the network (and after the Mac wakes). A *Connect* button sits on the copy; if the server refuses the saved password, automatic attempts stop (so the NAS never blocks the account) and the button asks for it once.
- Photos page: each member gets `Browse/<member>/Photos.html` on the copy — their protected photos browsable like in Photos (Years, Months, All Items, Favourites, Places, Albums, media types such as Live Photos, Portrait, Selfies, Videos, and Hidden behind a confirmation). It opens in Safari straight from the share, without the app or any server, and reads the originals in `objects/` directly. Thumbnails live in `metadata/thumbnails/`. Each Mac writes its own user's page, refreshed every half hour while the copy is connected; right-click a copy → *Open Photos Page*.
- Size, duration, location and media type of each photo are read from Photos, place names are looked up per ~10 km area, and favourites and albums of photos catalogued before 1.1 are recorded (and shared through the Vault journal like any other metadata).
- Security: another Mac's journal can no longer mark one of this Mac's own files as protected (a forged line could have made the app skip copying it), and file extensions from the journal are validated before they are used in a path.

## 1.2.3

- Updates are checked at every launch (and hourly while the app runs): a newer version is proposed right away instead of once a day.
- Browse integrity: the Vault view shows, per member and per copy, how many protected files are in `Browse/<member>/`, with *Show in Finder*; *Check Browse Folder* (right-click a copy, replaces *Rebuild*) verifies every link on disk, relinks missing ones and reports per member.

## 1.2.2

- A Mac that joins a Vault backs up its own photos first; other members' files (copied between copies) come after.
- A file another member's Mac has verified on a copy counts as protected there at once — no second read-back of the whole Vault by every Mac.
- Browse links are completed every pass in the background (files verified by another Mac, a member who joined), and old top-level year folders are swept until every Mac is on the new layout.

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
