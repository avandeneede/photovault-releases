# Photos Vault — Getting started

Ten minutes from install to a protected library.

## 1. Install

Download `PhotosVault-<version>.dmg` from the
[Releases page](https://github.com/avandeneede/photovault/releases/latest), open it and
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

## 3. Choose what to protect

Click **Add to Backup** in the toolbar:

- **Recent 200 Items** to see it work in a minute,
- **Entire Library** for everything (a first pass over a large library takes a few
  minutes; Photos itself limits how fast originals can be listed),
- **Custom Selection…** opens **Library**, where you can filter by date, kind, favourites
  or album and see how many items are already protected before adding the rest.

## 4. Let it run

Backups run automatically while the app is open. The **Overview** shows one line that
tells you where you stand — *Fully Protected*, *Protected on 1 of 2 Copies*, *No Storage
Copy Connected* — with progress and the files being copied (a few at a time, each on its
own track). Close the window: the Dock icon goes away and the app keeps going from the
menu bar icon next to the clock. Settings → General → *Open Photos Vault at login* makes
it permanent: after a restart there is only the icon, and it backs up on its own.

Unplug the disk in the middle: the copy shows *Not connected* and the number of items
waiting for it. Plug it back in: it catches up by itself.

## 5. Look at what is there

Right-click a copy → **Open Browse Folder in Finder**. Your photos are laid out by year and
month with their original names. Right-click → **Verify Integrity** re-reads every file on
that copy and repairs anything damaged from another copy.

## 6. Bring in the family

On another Mac, install Photos Vault, open **Storage Copies** and pick the same disk or NAS
folder: it appears under *Available Nearby* with a **Join** button, or add it manually. That
Mac joins your Vault as a member. Identical photos are stored once; everyone's photos end up
on every copy over time.

For a Mac in another house, run a Vault Service next to a copy:

```sh
photosvault serve /Volumes/Archive/PhotosVault
photosvault service token --replica /Volumes/Archive/PhotosVault --name Sarah --role member
```

and add it on the other side with *Add Storage Copy → Remote Vault Service…* using the
address, the token, and the certificate fingerprint the service printed.

## 7. Get something back

**Library** → filter → **Restore…**:

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

## Where things live

| What | Where |
|---|---|
| Your catalog (what is protected where) | `~/Library/Application Support/PhotosVault/catalog.sqlite` |
| The archive on each copy | `<copy>/objects/…` (content-addressed, read-only) and `<copy>/Browse/…` |
| Journals of each Mac | `<copy>/events/<device>.jsonl` |
| Tokens and certificate of a Vault Service | `~/Library/Application Support/PhotosVault/service/<copy id>/` |
| Keys and tokens | macOS Keychain |

Losing the catalog loses no media: every copy carries everything needed to rebuild it.
