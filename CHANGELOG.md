# Changelog

## 1.4.33

- **Lines a Mac rejected long ago are read again, once.** Before 1.4.6, about one signature in 2,000 was taken for forged (a rounding of the time) and the line rejected — and never read again, the journal cursor being past it. Anthony's journal holds 109 such lines (28 file hashes, 22 objects, 20 verifications, 39 favourites/albums): very likely the 51 files Sophie's Mac still showed as “not yet on the copy” after 1.4.31. Each Mac now reads every other Mac's journal again from the start, once per copy: lines it already knows are skipped, those it once rejected apply now. In the part it had read before, unsigned lines are left out without a warning (they were refused and reported then); a forged line further on is still reported.

## 1.4.32

- **Updates install by themselves again.** An update downloaded in the background was installed when the app quit — and Photos Vault lives in the menu bar and hardly ever quits (⌘Q only closes it there since 1.4.22). Updates waited for days, until Sparkle could no longer resume them: “Failed to resume installing update” on Sophie's Mac, stuck on 1.4.30. A downloaded update is now installed as soon as no file is moving — within the hour at most — and the app relaunches by itself.

## 1.4.31

- **A Mac joining the Vault sees everyone's photos as protected again.** 1.4.29 stopped accepting unsigned journal lines and had each Mac republish its old ones, signed, at the end of its journal. But the lines that followed them — “this file has this hash”, “this object is verified on the copy” — are read before those copies, when the file is not known yet, and had no effect: replayed on this Vault's real journals, a Mac joining would have seen Anthony at 14,361 of 106,914 files. Lines about a file or an object are now applied again, in their order, when that file or object is announced late; a catalog that already met the problem is repaired once (on that replay: 106,913 of 106,914). Very likely also why Sophie's Mac showed Anthony at 99 % (52 files): the repair runs there too.
- **No more Browse folder on a NAS.** On an SMB share, macOS stores a link as a small “XSym” text file that only the Mac that made it sees as a link — so 1.4.25's check, made on that Mac, passed, and Browse/ filled again with files nothing opens. Browse is now off on every SMB share, decided from the share itself, and the Vault section no longer shows Browse counts (“catching up”) for such a copy. On a NAS, browse with the Photos page.

## 1.4.30

- **The same 100 % on every Mac.** Files a Mac sets aside (iCloud would not send them) or skips are now announced in its journal: the other Macs count them out of that member's progress too. Sophie's Mac showed Anthony at 99 % — 106,910 of 106,914 files — for the 4 Live Photo videos his Mac had set aside; it now shows 100 %. Those files are not listed in the other Macs' Problems (it is not their business), and if the Mac they belong to stores one after all, it counts as protected everywhere. Files set aside before this version are announced once. Older versions simply ignore the new line.

## 1.4.29

- **No unsigned journal line is accepted any more.** Lines written before journals were signed (before 1.2.0) were still accepted, as long as their Mac had not yet been seen signing — so someone able to write a copy could slip unsigned lines at the start of the owner's journal and a Mac joining later took them for the owner's: claiming other members' photos in the owner's name, for instance. Every unsigned line is now refused. This Mac's own old lines — 164,955 here — are signed by it, with the same content, and written once more, signed, to the copies that hold them (84 MB on this NAS, once); a Mac joining later learns that history from them. Macs that already know those lines change nothing.

## 1.4.28

- **Security fix for 1.4.25–1.4.27.** To keep NAS recycle bins empty, those versions emptied a file before deleting or replacing it on a copy — with a call that follows symbolic links. Someone able to write to a copy could plant a link among its partial files pointing at a file of this Mac (the catalog, say), and the next clean-up would have emptied that file. Files are now emptied only when they are regular files, never through a link; the link itself is deleted, as before 1.4.25. On a Synology share like this one, links show up as plain files and were not followed; a USB disk could have carried real ones.

## 1.4.27

- **The Photos page is no longer rewritten just for its date.** 1.4.25 rewrote the page's data only when it changed — but its data carries the time it was built, so every build still differed: twice per build, 16.5 MB each time on this NAS (now 0 bytes in its recycle bin, but still sent). The build time is now left out of the comparison: a page whose photos did not change is not rewritten, and its *Updated* date is that of its last real change.

## 1.4.26

- **Duplicates are no longer uploaded to find out they are duplicates.** A file was hashed while it was sent to the copy, so one the copy already held went up whole and was then dropped — 43 GB from a family member's Mac on this Vault, at Wi-Fi speed. A file whose size matches a stored one is now read to the Mac first and hashed there; if the copy has those bytes, nothing is sent. Otherwise the local file is sent: still one read from Photos or iCloud.
- **Journal lines in the wrong file are refused.** Each Mac writes only its own journal on a copy; a line found in one Mac's journal but claiming to come from another was accepted. Such lines are now refused and counted in Activity's warning about rejected lines (none on this Vault: 922,273 lines checked).
- **Away from home, no automatic connection to the NAS.** A NAS share was mounted silently whenever possible — and away from home it was still tried every 15 minutes, offering the saved password's challenge response to whatever answered for that name on a café's or hotel's network. Automatic connection now happens only when the NAS announces itself over Bonjour, i.e. on its own network; *Connect* still works anywhere.

## 1.4.25

- **Quiet at rest.** A Mac with nothing left to send used half a core: the shield on the Overview pulsed for ever (the backup loop is always “running” in automatic mode), a pass ran every 3 s — reading every copy over the network, exchanging journals, re-checking the Browse folder — and statistics were recounted every 15 s. Now the shield moves only while files move; a pass that finds nothing waits longer before the next (up to 5 minutes) and any change — new photos, a copy connecting, *Retry* — starts one at once; the Browse folder is checked once per connection; statistics are recounted when something changed; and in the menu bar the app refreshes every 30 s instead of 3, so a NAS can sleep. Measured on this Mac, window open: 23 % of a core → 1 %.
- **No more NAS recycle bin full of backups.** A Synology keeps what a client deletes or replaces in `#recycle`: 149 GiB here — partial uploads, duplicates uploaded then dropped, replaced files and 430 old versions of the Photos page in 5 days. Files are now emptied before being deleted or replaced, so only 0-byte entries reach the bin, and the Photos page is only rewritten when its content changed (it never was “unchanged”: its data was written with keys in a random order).
- **A new disk fills from the NAS.** Photos' “this original is on the Mac” was the scan's answer, stale once Optimize Mac Storage sends originals back to iCloud (50,922 such files here): when the NAS holds the file, Photos is now asked at that moment, and the NAS used unless the original really is local. A NAS that connects while a disk fills becomes its source within a minute instead of at the next pass.
- **No Browse folder of unopenable files.** On a NAS share that stores links as small “XSym” text files, Browse/ filled with files nothing can open, and 238 names were retried on every pass. Such a share is now detected at the first link and gets no Browse folder, like an exFAT disk.

## 1.4.24

- **Browse Your Photos in the Vault has two buttons**: *Open in Library*, in the Photos Vault window as before, and *Open in Browser*, the same page — same fresh data, just as quick — in your web browser. Its address works while Photos Vault runs, from this Mac only.
- **Library looks like Photos**: inside the app, the page's sidebar and grid sit flush against the window, split by a hairline, instead of two floating cards on a pale background. In a browser, the page keeps its cards.

## 1.4.23

- Withdrawn: built from a base without 1.4.22's ⌘Q change, and published without these notes. Everything it had is in 1.4.24.

## 1.4.22

- **⌘Q leaves Photos Vault in the menu bar.** Quitting stopped the backup and took the icon away, when closing the app almost always means “out of my way”. ⌘Q (*Close to Menu Bar*) now closes the windows: the icon stays next to the clock and the Vault stays synchronized. To quit for real: ⌥⌘Q (*Quit Photos Vault*) or *Quit* in the icon's panel. A restart, a logout or an update still quit as before.

## 1.4.21

- **After the first backup: no more percentages, a shield with a check mark.** Percentages are for the first backup of a copy, which takes hours. Once a copy has held all your photos, new ones are routine: the menu bar icon turns and shows how many new items are on their way, the Overview says *Backing Up New Items* and lists the files being sent — then **Vault Synchronized**, with a checked shield, in the window and in the menu bar. Each copy remembers when its first backup was done; a new copy gets percentages again until it is full.
- **“Synchronized” no longer waits for other members' Macs.** On this Mac the copy said *Synced 2 months ago* and the app *Backing Up* for good: 15,473 of Sophie's files, which only her Mac can send, counted as work left. A copy is now up to date as soon as this Mac has nothing left to put on it; those files are mentioned in one line (“… files from other members' Macs are still on their way”) and no longer counted as *items waiting* on the copy, nor in the *connected — synchronizing N items* notification.
- **Back on the NAS's network, new photos are looked for at once** — when the share mounts — on top of being picked up as they arrive in Photos.

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
