# WoW 0.5.3 Alpha Client Patch – Enhanced WoWClient.exe (build 3368)

An improved **WoWClient.exe for World of Warcraft 0.5.3 alpha** (build 3368, 2003),
for players on alpha emulator servers such as those from The Alpha Project
(alpha-core). Smoother frames, higher FPS, fewer lag spikes and stutters, crash
fixes, a working login screen and no more freezing on exit – on modern
Windows 10 and Windows 11 PCs, laptops and desktops, with Nvidia, AMD or Intel graphics.

This repository contains **no game files** – only a small patch that turns the
WoWClient.exe you already have into the enhanced one. Download it under
**Releases** (WoW053_ClientPatch_v6.zip).

## What is improved from the original 0.5.3 client

**Smoother and faster**
- Smoother frames and higher frame rate: the original game clock moved in
  15.6 ms steps, so frames were uneven and the frame rate stayed around 64 fps.
- 1 ms timer resolution: shorter waits and faster loading.
- Fewer stutters and lag spikes when running into new areas: the game data is
  read into memory in the background right after start (lowest priority, at most
  half of the free memory). Helps most on hard disks and USB drives.
- Saving key bindings and addon settings no longer freezes the game.
- Much lower CPU and GPU use while the game is in the background.

**Stable**
- No more "Not responding" when you quit: the client always closes.
- Quit, Alt+F4 and the X button close the game at once.
- Crash fixes when loading maps and models.
- Fix for the "_Tls" startup error with Nvidia drivers.
- More usable memory (up to 4 GB instead of 2 GB, Large Address Aware).

**Convenient**
- Login screen with account name and password fields, also with the original
  interface.MPQ that has none.
- Laptops with two graphics chips (Nvidia Optimus, AMD switchable) use the fast one.
- Auto-run keeps going when you alt-tab.
- Buildings are always drawn, also far away.
- Free flying with .collision on servers that allow it.
- UI scale 0.8 at start.

**Clean**
- Read-only program code and a valid checksum.

## Supported clients

The patcher recognises these WoWClient.exe files and turns all of them into the
same enhanced file (SHA256 `94036EFFB22A19D0DA9B3A493AA77B4A865CE3ADBD225180D5E6EA1709D6E4FA`):

| Client | SHA256 |
|---|---|
| untouched Blizzard WoW 0.5.3 client | `861875776CE14A05FB49D4BB09F673D8A8939E2753372C3673AE6D43AC1A1C1F` |
| WoW 0.5.3 alpha client from the web archive (archive.org) | `38F4E97F5750BE226E2559F905E5BFCC7E79AA0D4EC9D51F7D147F1F0F551F3C` |
| WoW 0.5.3 client from The Alpha Project Discord | `EC4347715EC31BD3C67DEC98D17530F079E0374613D8A1A73F99B0893321F6D9` |
| WoW 0.5.3 Repack v6 | `1799003AB8ADE8D1E700AB1757AB331656DD5616D0E1DE53A0B1740E7346F715` |
| earlier improved client (v1) | `6B8B5E497DFFD617DED73F7B5A69E57A91CAA73FA47895398952594174EB6C84` |
| patch v3 | `E2DE2B6094F1EAF923C695F856346BB4230B45676B7730F463E05692CF8E8878` |
| patch v5 | `F7DC14C4A4CB293B12A16892C8CF032B0467C727E9E1329A5EF3EF272590B93E` |

Check yours in the game folder with `certutil -hashfile WoWClient.exe SHA256`.

## How to install

1. Download **WoW053_ClientPatch_v6.zip** from Releases and unpack it.
2. Copy `patch.bat`, `patch.ps1` and `gmod.dll` into your WoW 0.5.3 folder (next to WoWClient.exe).
3. Double-click `patch.bat`. It checks your file, keeps a backup
   (`WoWClient_before_patch.exe`), patches it and checks the result.

Or use the matching `.xdelta` file with xdelta UI, Delta Patcher or xdelta3.
Full instructions, undo and details are in `README.txt`.

**gmod.dll is needed.** gmod.dll (by rajkosto) is included with permission. It sends
the account name and password from the login screen to the server – without it
the game does not start and you cannot log in. The patcher copies it next to
WoWClient.exe if it is missing; an existing gmod.dll is never replaced.

## Laggy game or graphics errors? Use dgVoodoo2

On many computers the game runs much smoother with dgVoodoo2. The zip includes
the two files needed: copy `D3D9.dll` and `dgVoodoo.conf` from the `dgVoodoo2`
folder into the game folder. To go back, delete `D3D9.dll`.

The included `dgVoodoo.conf` already has `Mipmapping = autogen_bilinear`, which
fixes pink or purple edges on objects in the distance.

dgVoodoo2 is made by Dege: https://dege.freeweb.hu/ – all rights belong to him.

## Servers and community

- Host your own 0.5.3 server with The Alpha Project: https://github.com/The-Alpha-Project/
- Find servers and players in the community Discord: https://discord.gg/RzBMAKU
