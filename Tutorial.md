# Photos Vault — Getting started

Ten minutes from install to a protected library.

## 1. Install

Download `PhotosVault-<version>.dmg` from the
[Releases page](https://github.com/avandeneede/photovault-releases/releases/latest), open it and
drag **Photos Vault** into Applications.

The app is signed but not notarized through Apple's developer program, so the first
launch is blocked with *"Apple could not verify Photos Vault is free of malware"*. Once:

1. Click **Done** in that dialog (not *Move to Trash*).
2. Open **System Settings → Privacy & Security**, scroll to *Security*: *"Photos Vault"
   was blocked to protect your Mac* → **Open Anyway**, then authenticate.

Or, in Terminal: `xattr -dr com.apple.quarantine "/Applications/Photos Vault.app"`.
Later updates install through the app itself and do not trigger this again.

Launch it. macOS asks for access to your Photos library: choose **Allow Full Access** —
Photos Vault needs the originals, not the previews, and it only ever reads.

## 2. Add a storage copy

Go to **Storage Copies** → **Add Storage Copy** → *Folder on a Disk or NAS Share…* and pick
(or create) a folder on an external disk or a mounted NAS share, for example
`/Volumes/Archive/PhotosVault`. Give it a name.

This first copy creates your Vault. You can tick **Encrypt media in this Vault** here and
choose a passphrase; this cannot be changed later, and encrypted files are not browsable
in Finder. Most people leave it off.

Add a second copy the same way whenever you like — a NAS *and* an external disk is the
setup Photos Vault is designed around.

A NAS share only needs to be connected once. Afterwards the app reconnects it by itself
whenever the NAS is on the network, with the password saved in the Keychain. If the NAS
ever refuses that password, the copy shows **Connect** to ask for it again.

## 3. Choose what to protect

On first launch the Overview offers **Add Recent 200 Items**, to see it work in a minute,
and **Choose…**, which opens **Library → Selection**. There:

- **Recent 200**, **Recent 2,000** or **Entire Library** (a first pass over a large library
  takes a few minutes; Photos itself limits how fast originals can be listed). Entire
  Library also takes the photos of the shared albums you follow that are not in your
  library, and keeps everything current with a full pass once a day,
- or filter by kind, favourites, album and dates, see how many items are already
  protected, and add the rest.

## 4. Let it run

Backups run automatically while the app is open. The **Overview** shows one line that
tells you where you stand — *Fully Protected*, *Protected on 1 of 2 Copies*, *No Storage
Copy Connected* — and your photos on their way: **iCloud → This Mac → each copy**, with
what is still only in iCloud (Photos has to download it before the Mac can send it), the
speeds on the arrows, each copy's percentage and the time left. Below, the files being
copied, a few at a time, each with its speed. Close the window: the Dock icon goes away
and the app keeps going from the menu bar icon next to the clock, which shows the
percentage while a backup runs. Settings → General → *Open Photos Vault at login* makes
it permanent: after a restart there is only the icon, and it backs up on its own.

Unplug the disk in the middle: the copy shows *Not connected* and the number of items
waiting for it. Plug it back in: it catches up by itself.

## 5. Look at what is there

**Library** shows what is in the Vault, the way Photos does (**Overview → Browse Your
Photos in the Vault → Open** takes you there with the latest photos): years, months, favourites, places, albums and media types, with a
viewer for photos, videos and Live Photos (its Download button saves the original into
Downloads). The app serves this page from your Mac, so it is quick; the originals you open
come from the copy. Without the app — a new Mac, someone
else's computer — open `<your name> – Photos.html` at the root of the copy in Safari: the
same page, read straight from the share (slower).

None of this needs Apple or the Internet: the list comes from the catalog on your Mac and
the photos from the copy, over your home network. A photo deleted from Photos — by you, or
all at once if a library is wiped — stays in the Vault and moves to **Removed from Photos**
in the page's sidebar, out of the way of the others.

Right-click a copy → **Open Browse Folder in Finder**. Inside, one folder per family
member: yours holds your photos, laid out by year and month with their original names,
and nobody else's. **Vault** shows for each member how many of their protected files are
in that folder (*Show in Finder* opens it); **Check Browse Folder** (right-click a copy)
verifies every link on disk and repairs missing ones. Right-click → **Verify Integrity**
re-reads every file on that copy and repairs anything damaged from another copy.

## 6. Bring in the family

On another Mac, install Photos Vault, open **Storage Copies** and pick the same disk or NAS
folder: it appears under *Available Nearby* with a **Join** button, or add it manually. That
Mac joins your Vault as a member. Identical photos are stored once; everyone's photos end up
on every copy over time.

Your Mac then shows the new one in **Vault** with **Approve**: nothing it writes is used
until you approve it. Each member's progress and speed on every copy are listed there too.

For a Mac in another house, run a Vault Service next to a copy:

```sh
photosvault serve /Volumes/Archive/PhotosVault
photosvault service token --replica /Volumes/Archive/PhotosVault --name Sarah --role member
```

and add it on the other side with *Add Storage Copy → Remote Vault Service…* using the
address, the token, and the certificate fingerprint the service printed.

## 7. Get something back

**Library → Selection** → filter → **Restore…**:

- **To a Folder…** writes the originals as real files grouped by month, from the fastest
  connected copy. Existing files are never overwritten.
- **Back Into Photos…** re-imports them into your Photos library with their favourite state
  and albums (matched by name). Photos does not detect items that are already there, so
  only do this for items you actually lost.

## 8. Day to day

- New photos join the backup by themselves (Settings → *Protect new photos and videos as
  they arrive*); edits and deletions are tracked too, without rescanning.
- **Problems** lists files that failed after several attempts, with the reason. *Retry* or
  *Skip*. The Overview links there when something needs you.
- Right-click a copy → **Verify Integrity** re-reads everything on it; anything damaged is
  repaired from another copy.
- Settings: pause on battery, limit copy speed, notifications, Touch ID lock, updates.

## A typical setup: NAS + external disk

1. Add the NAS share as the first copy; let the first backup run overnight.
2. Add an external disk as the second copy: it fills **from the NAS**, not from iCloud, at
   disk speed. Keep it in a drawer; plug it in once a month — it catches up in minutes
   and tells you when it is up to date.
3. If the NAS dies, the disk holds everything; if the disk is stolen, the NAS does. A new
   NAS is just a new copy: it fills from the disk.

## When things go wrong

| You see | It means | What to do |
|---|---|---|
| *Not connected* | The disk is unplugged or the NAS is out of reach | Nothing. It catches up when back. |
| *Waiting for storage* on files | No connected copy can take them right now | Connect a copy. |
| *Full* | The disk has no room left | Free space or add a bigger copy; other copies keep working. |
| *Needs attention* on a copy | Wrong passphrase, wrong Vault, rejected token, changed certificate | Read the detail on the row; usually enter the passphrase or re-add the copy. |
| A file in **Problems** | Photos could not hand it over, or the copy refused it | Retry later; skip if the item is gone for good. |
| *Photos no longer remembers what changed* | The Mac was away too long | Library → Entire Library, once. |
| *… lines in other members' journals were rejected* | A line claims to come from another member's Mac but its signature does not match | Nothing: those lines are ignored. If the number keeps growing, check who can write to the share. |

## Where things live

| What | Where |
|---|---|
| Your catalog (what is protected where) | `~/Library/Application Support/PhotosVault/catalog.sqlite` |
| The archive on each copy | `<copy>/objects/…` (content-addressed, read-only) and `<copy>/Browse/…` |
| Journals of each Mac | `<copy>/events/<device>.jsonl` |
| Each member's Photos page | `<copy>/<member> – Photos.html`, its data in `<copy>/.photos/<member>/`, thumbnails in `<copy>/metadata/thumbnails/` |
| Tokens and certificate of a Vault Service | `~/Library/Application Support/PhotosVault/service/<copy id>/` |
| Keys and tokens | macOS Keychain |

Losing the catalog loses no media: every copy carries everything needed to rebuild it.
