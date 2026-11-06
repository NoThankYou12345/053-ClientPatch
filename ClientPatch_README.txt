WoWClient.exe improvement patch for World of Warcraft 0.5.3 (build 3368)
=======================================================================

This package contains no game files, only a small patch that is applied to the
WoWClient.exe you already have, plus gmod.dll and dgVoodoo2. Two ways to apply
it are included: an automatic patcher (patch.bat) and xdelta patches.

What is better than the original 0.5.3 client
---------------------------------------------
Smoother and faster
- Smoother frames and higher frame rate: the original game clock moved in
  15.6 ms steps, so frames were uneven, every hitch was rounded up and the frame
  rate stayed around 64 fps. The clock now runs smoothly between those steps.
- 1 ms timer resolution: shorter waits and faster loading.
- Fewer stutters when you run into new areas: right after start the game's data
  files are read once in the background at the lowest priority, so they are
  already in memory when the game needs them. It uses at most half of the free
  memory and skips this on computers with little free memory. This helps most
  when the game is on a hard disk or a USB drive.
- Saving key bindings and addon settings writes the file at once instead of
  line by line, so it no longer freezes the game on a slow disk.
- Much lower CPU and graphics card use while the game is in the background.

Stable
- Quit never hangs: if the client gets stuck while closing, it is ended after
  8 seconds instead of staying on "Not responding".
- Quit, Alt+F4 and the X button close the game at once.
- Crash fixes when loading maps and models.
- Fix for the "_Tls" startup error on Nvidia drivers.
- More usable memory (up to 4 GB on 64-bit Windows instead of 2 GB).

Convenient
- Laptops with two graphics chips use the fast one (no effect on desktops).
- Auto-run keeps going when you alt-tab.
- Buildings are always drawn, also far away (no buildings popping in).
- Free flying with .collision on servers that allow it.
- UI scale 0.8 at start (the console command "scaleui" still works).
- Login screen with account name and password fields, also with an original
  interface.MPQ that has none (patch.bat also updates an original
  Data\interface.MPQ, which adds Fullscreen/Windowed in Video Options).

Clean
- The program code is read-only and the file has a valid checksum.
- No packed, encrypted or obfuscated content (the login-screen fallback text
  is stored as plain text in its own section).

gmod.dll
--------
gmod.dll (by rajkosto) is included with permission. It sends the account name
and password from the login screen to the server - without it you cannot log in to
0.5.3 servers, and the game does not start. The patcher copies it next to
WoWClient.exe if it is missing; an existing gmod.dll is never replaced.

How to install
---------------
Option 1: automatic patcher (recommended)
-----------------------------------------
1. Unpack the zip and drop everything into the game folder (next to WoWClient.exe).
2. Double-click patch.bat.
   It checks which WoWClient.exe you have, saves a backup
   (WoWClient_before_patch.exe), patches it and checks the result.
   An unknown file is never changed; its SHA256 is shown instead.
   It also updates an original Data\interface.MPQ, and copies gmod.dll,
   D3D9.dll and dgVoodoo.conf into the game folder if they are missing there.
   Files that are already there are never replaced.
If Windows blocks the files: right-click each file > Properties > Unblock.

Option 2: xdelta
-----------------
Use the file in the xdelta folder that matches your WoWClient.exe:
    web-archive_to_patched.xdelta          web archive client
    repack-v6_to_patched.xdelta            Repack v6 client
    untouched-blizzard_to_patched.xdelta   untouched Blizzard client
    enhanced-v5_to_patched.xdelta          first v5 release
    unknown-variant-1_to_patched.xdelta    unidentified client variant 1
    unknown-variant-2_to_patched.xdelta    unidentified client variant 2
With a patch program that reads xdelta/VCDIFF files (for example xdelta UI or
Delta Patcher): source file = your WoWClient.exe, patch = the .xdelta file.
With xdelta3 on the command line, in the game folder:
    xdelta3 -d -s WoWClient.exe web-archive_to_patched.xdelta WoWClient_patched.exe
Then rename WoWClient.exe to WoWClient_before_patch.exe and
WoWClient_patched.exe to WoWClient.exe. Check the result with certutil (see
below): it must be 767F08B7...EAEA7C.
Two more clients (earlier improved client v1, patched with patch v3) and the
Alpha Project Discord client are supported by the automatic patcher
(Option 1) but do not yet have an xdelta file here - use Option 1 for those.

Undo
----
Delete WoWClient.exe and rename WoWClient_before_patch.exe to WoWClient.exe.

Supported WoWClient.exe (all become the same file)
--------------------------------------------------
untouched Blizzard 0.5.3 client        861875776CE14A05FB49D4BB09F673D8A8939E2753372C3673AE6D43AC1A1C1F
0.5.3 client from the web archive     38F4E97F5750BE226E2559F905E5BFCC7E79AA0D4EC9D51F7D147F1F0F551F3C
0.5.3 Repack v6 client                1799003AB8ADE8D1E700AB1757AB331656DD5616D0E1DE53A0B1740E7346F715
earlier improved client (v1)          6B8B5E497DFFD617DED73F7B5A69E57A91CAA73FA47895398952594174EB6C84
patched with patch v3 (update)        E2DE2B6094F1EAF923C695F856346BB4230B45676B7730F463E05692CF8E8878
first v5 release                      F7DC14C4A4CB293B12A16892C8CF032B0467C727E9E1329A5EF3EF272590B93E
The Alpha Project Discord client      EC4347715EC31BD3C67DEC98D17530F079E0374613D8A1A73F99B0893321F6D9
unidentified client variant 1         77868439C6FE23A98E572FBD5196D28C543CFB6D0B0E6E5035D00E24E030CA6A
unidentified client variant 2         0B7E4526BFF2428C74F0A9146502E847BE3484D7856B89BBC31DFB6A97D539B2
Result after patching                 767F08B7F62F7618FCB3AB401028701E122B3078A28C5DAD33B3BE43E4EAEA7C

To see which one you have, open a command prompt in the game folder and type:
    certutil -hashfile WoWClient.exe SHA256

dgVoodoo2
---------
On many computers the game runs much smoother with dgVoodoo2, so D3D9.dll and
dgVoodoo.conf from dgVoodoo2 2.86.5 are included. If the game runs worse with
it, delete D3D9.dll from the game folder.
The included dgVoodoo.conf has Mipmapping = autogen_bilinear under [DirectX],
which fixes pink or purple edges on objects in the distance.
dgVoodoo2 is made by Dege (https://dege.freeweb.hu/); all rights belong to him.

Changes
-------
- Smoother clock without the frame rate limit of v3/v4 (the limit made frames
  less even on some computers).
- Background reading of the game data, one-write saving of key bindings, and
  the quit watchdog (see above).
- All own values kept in a separate memory area that nothing else can use.
- Account name and password fields on the login screen, also with an original
  interface.MPQ.
- The login-screen fallback data moved into its own section with ordinary
  code/data flags, instead of a single appended cave, to avoid being flagged
  as suspicious by antivirus heuristics.
