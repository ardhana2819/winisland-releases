# WinIsland

A small Windows 11 overlay inspired by the iPhone Dynamic Island. A black pill at the top center of the screen shows the time, the music that is playing (Spotify, YouTube, Apple Music, ...), and WhatsApp, Discord and other apps' messages, so you can see them in a game without alt-tabbing.

This repository holds only the downloads. The source code is private.

## Status

**Beta (v1.8.1-beta.1).** WinIsland is ready to use and installs like a normal app, but it is still a beta. It shows the island with a clock at the top of the screen, a tray icon (Pause for 1 hour or Resume, Hide or Show island, Settings, Quit; dimmed while paused), the hotkeys Ctrl+Alt+H (hide or show) and Ctrl+Alt+I (expand), the current song from any media app (music players before videos) with play, pause, next, previous, seek and that app's volume, colored from the song's artwork, also when paused or with an empty view when nothing plays, an orange or green dot while an app uses the microphone or camera, WhatsApp, Discord and (if turned on) other apps' notifications with their logos (banner, +N, the last 3 chats as stacked cards that open to their last 3 messages, Alt+X to hide, a small white dot on the island for ones you have not seen yet, and a banner while a WhatsApp Web call rings), emoji in color, an expanded island with a music page and a notifications page (scroll, Alt+Up and Alt+Down, or the page dots, which show while the page changes), and a Settings window (tray > Settings) that sets the island size (Small to Extra large), the look (Solid, or Glass in beta), whether hiding a banner also clears it from Windows, and start with Windows.

## How light is it?

WinIsland is meant to sit on screen all day, also while you play, so it was built to use as little of the PC as possible. These numbers were measured on the PC it was made for (Intel Core i5-9400F with 6 cores, 16 GB of memory, GeForce GTX 1650 Super, Windows 11), with the island showing the clock, Glass look, Extra large size, on 4 Nov 2026.

| What | Measured | What it means |
|---|---|---|
| Processor (CPU) while idle | 0.05 to 0.09 % | Less than a tenth of one percent of the processor: in practice, nothing. |
| Processor when a message arrives | 4 to 6 % for a moment | The banner's short animation; it drops back to almost zero right after. |
| Memory (RAM) | about 127 to 135 MB right after it starts, of which 45 to 55 MB is WinIsland's own; about 140 to 155 MB after it has been used for a while | Less than 1 % of 16 GB. The part that is not WinIsland's own is mostly Windows' shared program parts, which other apps load too. After use, .NET keeps a little more memory ready, and it goes up and down a few MB as .NET tidies up; it does not keep growing. |
| Video memory (graphics card) | 0 MB | The island is drawn by the processor, not the graphics card, so it takes nothing away from your games. With the Glass look, the blur behind it is drawn by Windows itself, which draws your screen anyway. |
| Start-up | about 1.7 s of processor time | Spread over the first seconds after Windows starts. |
| Network | none | WinIsland never goes online. |

**In short:** WinIsland is very light. While it waits, it uses almost no processor time; it takes about 1 % of the memory on a 16 GB PC and no graphics card memory at all. On a PC like the one above you should not notice it in games or daily work. On a slower PC or one with less memory it still uses the same small amounts, so it takes a bigger share there.

## Requirements

- Windows 11 (64-bit).
- Games in **windowed or borderless** mode. Exclusive fullscreen is not supported. In exclusive fullscreen, Discord also shows messages only in its own in-game overlay, so they do not reach the island.
- Music from any app that tells Windows what it plays: Spotify, YouTube or YouTube Music in a browser, Apple Music, and others. The volume button on the music page changes only that app's volume; for a browser that is every tab together. Firefox shows its music but gets no volume slider, because it does not name itself to Windows the usual way.
- For notifications: WhatsApp Web installed as an app from Chrome (Chrome menu > Cast, save and share > Install page as app), or WhatsApp desktop from the Microsoft Store, and Discord desktop. With both WhatsApp apps open, WinIsland shows each message once, from WhatsApp Web.
- Incoming call banner: WhatsApp Web only, with WhatsApp set to English. In another language, calls show as normal message banners.

## Install

1. Open **[Releases](../../releases)** and download `WinIsland-<version>-setup.exe` from the newest release. No sign-in is needed. Beta releases are marked **Pre-release**.
2. Run it. The setup is not signed, so Windows SmartScreen warns once per version: click **More info** > **Run anyway**.
   It installs WinIsland for your Windows account only, without administrator rights, into `%LOCALAPPDATA%\Programs\WinIsland`, adds it to the Start menu, and offers to start it. No .NET install is needed.
3. To pin it: Start > All, right-click WinIsland > Pin to Start. It starts with Windows from the first run on (switch it off in Settings).
4. **Optional: instant notifications.** Without this step WinIsland checks notifications once per second; with it they arrive in about a tenth of a second. It gives WinIsland "package identity" with a personal signing certificate, trusted once as administrator. The steps are in `README.md` inside `%LOCALAPPDATA%\Programs\WinIsland\packaging`, next to the scripts.

**Updating:** the **Update** button in WinIsland's Settings (and Start > **Update WinIsland**) does not work with this repository. To update, download the newer `setup.exe` from Releases and run it. It closes WinIsland for a moment, updates it in place, keeps your settings and starts it again.

**Without the installer:** each release also has `WinIsland-<version>-win-x64.zip` (about 83 MB). Right-click it > **Properties** > tick **Unblock** > OK (without this the setup scripts are refused), unzip it to a folder you keep, then in its `packaging` folder right-click `Add-StartMenuShortcut.ps1` > **Run with PowerShell** to add it to the Start menu. Use either the installer or the zip on one PC, not both.

## First run

1. **Allow notification access.** WinIsland asks once. You can change it later in Windows Settings > Privacy & security > Notifications.
2. **Turn off Windows banners for WhatsApp and Discord**, so you do not see each message twice. Keep the notification center on, because that is where WinIsland reads them from.
   Windows Settings > System > Notifications > WhatsApp (and then Discord) > turn off **Show notification banners**, keep **Show notifications in notification center** on.
   Do this in **Windows Settings only**. Keep notifications turned on inside WhatsApp and Discord themselves (in WhatsApp: Settings > Notifications > Show notification banner = Always). If an app's own setting is off, it never sends the notification to Windows, so WinIsland cannot see it either.
   Alternative: Windows **Do not disturb** also hides the banners while WinIsland still receives the notifications.

## Uninstall

**Installed with the setup:** Windows Settings > Apps > Installed apps > WinIsland > **Uninstall**. It closes WinIsland and removes its files, the Start menu shortcut, the start with Windows entry, and the instant notifications package. Two things stay on purpose:

- `%USERPROFILE%\.winisland`, with `settings.json` and `winisland.log` (never message text), so a later install keeps your settings. Delete the folder yourself if you want them gone.
- The signing certificate, if you set up instant notifications, because removing it needs administrator rights. Only if you want it gone: in PowerShell opened as administrator, run
  `Get-ChildItem Cert:\LocalMachine\TrustedPeople | Where-Object Subject -eq "CN=WinIsland Dev" | Remove-Item`
  If you created the certificate on that PC, also remove its private key, in a normal PowerShell:
  `Get-ChildItem Cert:\CurrentUser\My | Where-Object Subject -eq "CN=WinIsland Dev" | Remove-Item`

Windows may still list WinIsland under Settings > Privacy & security > Notifications. That entry is only the permission you gave and does nothing without the app.

**Installed from the zip:** there is no entry in Installed apps. Do these steps in this order:

1. **Turn off start with Windows:** tray icon > Settings > switch off start with Windows > Save. If you skip it, Windows keeps a harmless startup entry that points at a missing file.
2. **Quit WinIsland:** tray icon > Quit.
3. **Remove the Start menu shortcut:** open PowerShell in the WinIsland folder's `packaging` folder (in File Explorer: right-click the folder > Open in Terminal) and run `.\Add-StartMenuShortcut.ps1 -Remove`
4. **Only if you set up instant notifications:** in the same folder, run `.\Unregister-IdentityPackage.ps1 -PackageName WinIsland`
5. **Delete the WinIsland folder**, and if you want, `%USERPROFILE%\.winisland` and the certificate as above.

If you already deleted the folder first, the startup entry can be removed in PowerShell:
`Remove-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name WinIsland`
and the shortcut by deleting `WinIsland` from `%APPDATA%\Microsoft\Windows\Start Menu\Programs`. An identity package can still be removed with `Get-AppxPackage WinIsland | Remove-AppxPackage`.

## Privacy

- WinIsland makes **no network calls**.
- Music information comes only from the Windows media session. WinIsland never signs in to Spotify.
- Notifications are read only through the Windows notification listener, and only after you allow it.
- Message text stays **in memory only**. It is never written to disk or to logs. Logs hold event types and errors only.
- Settings are saved in `%USERPROFILE%\.winisland\settings.json`: hotkeys, which apps show, banner time, hide message text, also clear from Windows, island size, look (Solid or Glass), start with Windows. Next to it, `winisland.log` (at most 256 KB) records event types and errors only, never message text. Nothing else is written to disk.
- No screen capture, no reading other programs' memory, no injection or hooks into games.
- The orange dot asks Windows' audio system whether another app is recording, and the green dot reads Windows' own record of camera use. WinIsland never opens the camera or microphone and records nothing. The camera dot is untested, because it was built without a webcam. The Glass look's blur is drawn by Windows itself; WinIsland never sees what is behind the island.
- WinIsland never deletes anything from Windows unless you turn on **Also clear from Windows notification center** in Settings (off by default). Then hiding a banner with a swipe or the hide hotkey also removes that chat's notifications from the Windows notification center.

## License

Copyright (c) 2026 Diva. All rights reserved. You may download and use the released app for personal use. The app and its files may not be redistributed, modified or sold.
