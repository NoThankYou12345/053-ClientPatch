WoWClient.exe patch for World of Warcraft 0.5.3 (build 3368)
============================================================

This package contains no game files, only a small patch (about 1-2 KB) that is
applied to the WoWClient.exe you already have. Two ways to apply it are
included: an automatic patcher (patch.bat) and xdelta patches.

What it does
------------
- Smoother frames: the game clock moved in 15.6 ms steps, so frames were uneven
  and every hitch was rounded up. It now runs smoothly between those steps.
- Frame rate limit = the refresh rate of the monitor the game is on (follows the
  window to another monitor), at most 144 fps.
- Laptops with two graphics chips use the fast one (no effect on desktops).
- 1 ms timer resolution: faster loading and shorter waits.
- Much lower CPU/GPU use while the game is in the background; auto-run keeps
  going when you alt-tab.
- Quit, Alt+F4 and the X button close the game at once (no more freezing on exit).
- Minimap correct inside buildings and caves.
- UI scale 0.8 at start (the console command "scaleui" still works).
- Free flying with .collision on servers that allow it, the Nvidia "_Tls"
  startup error fix, crash fixes when loading maps and models, longer view
  distance, more usable memory (these are included for the web archive client
  too).
- Read-only code section and a valid PE checksum.

Supported WoWClient.exe (all become the same file)
--------------------------------------------------
0.5.3 client from the web archive  38F4E97F5750BE226E2559F905E5BFCC7E79AA0D4EC9D51F7D147F1F0F551F3C
0.5.3 Repack v6 client             1799003AB8ADE8D1E700AB1757AB331656DD5616D0E1DE53A0B1740E7346F715
earlier improved client (v1)       6B8B5E497DFFD617DED73F7B5A69E57A91CAA73FA47895398952594174EB6C84
Result after patching              E2DE2B6094F1EAF923C695F856346BB4230B45676B7730F463E05692CF8E8878

To see which one you have, open a command prompt in the game folder and type:
    certutil -hashfile WoWClient.exe SHA256
The patched client needs gmod.dll in the game folder; both clients above
already have it.

Option 1: automatic patcher (recommended)
-----------------------------------------
1. Copy patch.bat and patch.ps1 into the game folder (next to WoWClient.exe).
2. Double-click patch.bat.
   It checks which WoWClient.exe you have, saves a backup
   (WoWClient_before_patch.exe), patches it and checks the result.
   An unknown file is never changed; its SHA256 is shown instead.
If Windows blocks the files: right-click each file > Properties > Unblock.

Option 2: xdelta
----------------
Use the file in the xdelta folder that matches your WoWClient.exe:
    web-archive_to_patched.xdelta          web archive client
    repack-v6_to_patched.xdelta            Repack v6 client
    earlier-improved-v1_to_patched.xdelta  earlier improved client (v1)
With a patch program that reads xdelta/VCDIFF files (for example xdelta UI or
Delta Patcher): source file = your WoWClient.exe, patch = the .xdelta file.
With xdelta3 on the command line, in the game folder:
    xdelta3 -d -s WoWClient.exe web-archive_to_patched.xdelta WoWClient_patched.exe
Then rename WoWClient.exe to WoWClient_before_patch.exe and
WoWClient_patched.exe to WoWClient.exe. Check the result with certutil (see
above): it must be E2DE2B60...8878.

Undo
----
Delete WoWClient.exe and rename WoWClient_before_patch.exe to WoWClient.exe.

Optional: dgVoodoo.conf (for clients with dgVoodoo2, e.g. the Repack)
---------------------------------------------------------------------
optional\dgVoodoo.conf is the Repack's dgVoodoo2 settings file with two changes:
- [DirectX] Resolution = unforced (the Repack forces 1600x1200, which moves the
  mouse position on the world map; zone highlight and clicks land wrong).
- ForceVerticalSync = false, so the frame rate limit above paces the frames.
  Set it back to true if you prefer V-Sync.
Copy it over the dgVoodoo.conf in the game folder if you want these changes.
