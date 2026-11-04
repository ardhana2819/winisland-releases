# WinIsland

A small Windows 11 overlay inspired by the iPhone Dynamic Island. A black pill at the top center of the screen shows the time, the music that is playing (Spotify, YouTube, Apple Music, ...), and WhatsApp, Discord and other apps' messages, so you can see them in a game without alt-tabbing.

This repository holds only the downloads. The source code is private.

## Requirements

- Windows 11 (64-bit).
- Games in **windowed or borderless** mode. Exclusive fullscreen is not supported.
- Music from any app that tells Windows what it plays: Spotify, YouTube or YouTube Music in a browser, Apple Music, and others.
- For notifications: WhatsApp Web installed as an app from Chrome (Chrome menu > Cast, save and share > Install page as app), or WhatsApp desktop from the Microsoft Store, and Discord desktop.

## Install

1. Open **[Releases](../../releases)** and download `WinIsland-<version>-setup.exe` from the newest release. Beta releases are marked **Pre-release**.
2. Run it. The setup is not signed, so Windows SmartScreen warns once per version: click **More info** > **Run anyway**.
   It installs WinIsland for your Windows account only, without administrator rights, and adds it to the Start menu. No .NET install is needed.
3. On the first run, allow notification access when WinIsland asks.
4. Turn off Windows banners for WhatsApp and Discord so you do not see each message twice: Windows Settings > System > Notifications > WhatsApp (and then Discord) > turn off **Show notification banners**, keep **Show notifications in notification center** on. Keep notifications turned on inside WhatsApp and Discord themselves.

**Without the installer:** each release also has `WinIsland-<version>-win-x64.zip`. Right-click it > **Properties** > tick **Unblock** > OK, unzip it to a folder you keep, then in its `packaging` folder right-click `Add-StartMenuShortcut.ps1` > **Run with PowerShell**. Use either the installer or the zip, not both.

## Updating

The **Update** button in WinIsland's Settings does not work with this repository. To update, download the newer `setup.exe` from Releases and run it. It updates WinIsland in place and keeps your settings.

## Uninstall

Windows Settings > Apps > Installed apps > WinIsland > **Uninstall**. Your settings stay in `%USERPROFILE%\.winisland`; delete that folder if you want them gone.

## Privacy

WinIsland never goes online. It reads music from Windows' media controls and notifications from Windows' notification center, with your permission. Message text stays in memory only and is never written to disk or logs.

## License

Copyright (c) 2026 Diva. All rights reserved. You may download and use the released app for personal use. The app and its files may not be redistributed, modified or sold.
