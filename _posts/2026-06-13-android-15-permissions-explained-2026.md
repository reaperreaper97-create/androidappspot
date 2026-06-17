---
layout: post
title: "Android 15 Permissions Explained: What Each Toggle Actually Does"
description: "A clear breakdown of every Android 15 runtime permission — what data it exposes, when to grant it, and how partial permissions work."
date: 2026-06-13 11:00:00 -0700
author: "Android Apps Spot"
permalink: /android-15-permissions-explained-2026/
---

Android 15 introduced finer-grained permission controls than any previous version. The catch is that most users still grant everything on first launch because the wording in the prompt is vague. Here's what each permission actually exposes — and where the new partial-grant options live.

## The Two Permission Tiers

**Install-time permissions** are granted automatically when you install the app. They're listed on the Play Store page under "App permissions." You can't deny them individually — the only way to refuse is to not install.

**Runtime permissions** are the dialogs you see at first use. These you control. Android 15 splits some of them into "while using the app," "only this time," and "deny."

## Location

| Grant | What the app sees |
|---|---|
| Precise, always | GPS to ~3 m, all the time |
| Precise, while using | GPS to ~3 m, only when app is in foreground |
| Approximate, while using | City-level only (~3 km accuracy) |
| Only this time | One-shot, revoked when app closes |
| Deny | Nothing |

Android 15 adds a per-session toggle: when you re-open an app you previously granted "only this time," it asks again. Use **Approximate** for weather, food delivery, anything that doesn't need your house number.

## Camera & Microphone

Both now have a system-wide kill switch in Quick Settings (since Android 12, still works in 15). Tap the camera or mic icon in the notification shade → off → no app on the phone can use them until you toggle back on.

In-app: prefer **only this time** for one-off uses (scanning a QR code, recording a single voice note).

## Photos and Videos

Android 14 replaced "Read external storage" with a media picker. Android 15 added **partial access**: when an app requests photos, the dialog now offers "Select photos" — you pick the specific images you want to share, and the app sees only those. The app never gets a list of your gallery.

Always pick **Select photos** unless the app is your trusted gallery / cloud-backup tool.

## Contacts

Granular control was added in 15 — you can now share a single contact (e.g., when an app asks for "emergency contact"). When the app requests `READ_CONTACTS`, look for **Share one contact** in the dialog.

## Notifications

Since Android 13, apps must request permission to send notifications. In Android 15 there's a new **categorized** view: Settings → Notifications → per-app → you see the notification channels the developer registered (Promotions, Updates, Chat). Disable Promotions, keep Chat.

## Nearby Devices

Used by Bluetooth audio, smart home apps, and (for some reason) most ad networks for cross-device tracking. Grant only to apps that actually pair with hardware (Spotify for car stereo, Strava for HR strap).

## Body Sensors

Heart rate, step count, accelerometer. Wearable companion apps need it. Most other apps requesting it are profiling user activity for analytics — deny.

## SMS & Phone

The big ones to think hard about. `READ_SMS` lets the app read every text including 2FA codes; `RECEIVE_SMS` lets it intercept them. Only your default SMS app (Messages, Signal, etc.) should ever have this. Banking apps sometimes request it for "auto-fill OTP" — refuse, and type the code manually.

## Accessibility Services

Not in the standard permission dialog. Lives in **Settings → Accessibility → Installed apps**. Accessibility Services can see and click on anything on your screen, including passwords. Only enable for apps you fully trust: TalkBack, switch control, a known password manager.

## "Display Over Other Apps" and "Install Unknown Apps"

Special access permissions in Settings → Apps → Special access. **Display over other apps** is what enables Facebook Messenger Chat Heads — and also what malware uses to overlay phishing dialogs on top of banking apps. Grant sparingly.

## Reviewing What You've Already Granted

Settings → Privacy → Permission manager. Group by permission (e.g., "Camera: 14 apps with access") — then revoke any app you don't recognize using that capability. Do this once a quarter.

---

The default in Android 15 is closer to "least privilege" than ever before. The system gives you the tools — the only thing it can't do is read the prompts for you.
