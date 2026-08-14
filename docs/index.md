---
layout: docs
title: Documentation
heading: How AdultXBlocker works, end to end.
eyebrow: Documentation
description: >-
  Set up AdultXBlocker, lock an iPhone or iPad with a Screen Time passcode you
  never see, manage your locked devices, and understand exactly what the
  extension can and cannot access.
lede: >-
  Everything the extension does, in the order you'll meet it. If something here
  doesn't match what you're seeing, email us — that's a documentation bug and we
  want to know.

faqs:
  - q: What happens if I lose the passcode?
    a: >-
      You never had it. It's generated, encrypted, and backed up to your account
      *before* it's shown, and it's only ever shown one keypad tap at a time.
      Recovering it is a normal, expected thing to do — not an emergency.
  - q: Does this work on Android or Windows?
    a: >-
      Not today. AdultXBlocker walks you through iOS Screen Time, so the device
      being locked is an iPhone or iPad. The extension itself runs in Chrome on
      any desktop operating system.
  - q: What if I close the popup halfway through setup?
    a: >-
      Chrome destroys extension popups whenever they lose focus, so your setup is
      cached and picks up where it left off. A device left mid-setup shows as
      **Pending** in your device list and can be resumed days later.
  - q: Do I need an account?
    a: >-
      Yes — a verified email and password. That account is what the encrypted
      passcode backup belongs to, and it's what lets you see your devices from a
      different computer.
  - q: What data does the extension collect?
    a: >-
      The extension requests one Chrome permission: `storage`. It never asks for
      your tabs, your browsing history, Google Drive, or access to your files.
  - q: Can I unlock a device before its time is up?
    a: >-
      Only by spending one of your three **rescue passes**. Three per account,
      ever — they don't reset and can't be topped up. You can also switch rescue
      off permanently, after which nothing opens a lock early.
  - q: Is there a paid plan?
    a: >-
      No. Every account is on the Free plan and there is nothing to buy.
---

## Before you start

AdultXBlocker is a **commitment device**, not a content filter. It doesn't
inspect pages, watch traffic, or run on the device it protects. What it does is
walk you through turning on iOS Screen Time's content restrictions using a
passcode that is generated randomly, shown to you only as a sequence of keypad
taps, and never displayed as a number you could memorise.

You'll need three things:

- **Chrome on a desktop**, with the extension installed.
- **The iPhone or iPad you want to lock**, in your hand — you'll be typing on it.
- **An email address you can receive mail at**, to verify your account.

Setting up takes about five minutes, and roughly thirty seconds of that is the
part you can't pause.

## Creating your account

Sign in with an email address and password before starting setup. The email must
be verified before the extension will talk to the backup service — an unverified
account can't reach cloud storage at all.

That account is what your encrypted passcode backups belong to. Signing in on a
different computer shows you the same list of devices, which matters if the
laptop you set things up on isn't the one you have when the lock expires.

Every account is on the Free plan. There are no other account types.

## Locking a device

The order of operations here is deliberate, and it's worth understanding before
you start.

**1. Name the device.** Give it a display name and a device type, so the list
means something later when there's more than one.

**2. The extension generates a passcode — and backs it up first.** It creates a
random Screen Time passcode, sends it to our server, and the server encrypts it
and saves the device with the status **Pending**. Only *then* does the
thirty-second countdown begin. Nothing is shown to you until the backup already
exists, so an interruption can never strand you with a passcode nobody has.

**3. Thirty seconds of keypad instructions.** The digits are played one keypad
tap at a time, mixed with decoy taps, so watching the screen doesn't tell you the
passcode. You follow along on the device.

**4. Screen Time restrictions go on.** At this point the passcode exists in
exactly one place: encrypted, on the server, under your account.

**5. Confirm, and choose how long.** The duration is asked at the *end*, not the
start. Once you confirm, the device moves from **Pending** to **Locked** and the
unlock time is set to that many days from that instant.

That last point is the one people ask about. Setup can be abandoned on a Tuesday
and resumed the following week, so a deadline set when setup *started* would have
quietly eaten days you never actually spent locked. The clock starts when the
lock does.

One lock day means exactly twenty-four elapsed hours. That stays true across
time zones and daylight-saving changes.

## If the popup closes mid-setup

Chrome destroys an extension popup whenever it loses focus. That's normal
behaviour, not a bug, and the extension is built around it.

Your progress is cached, so reopening the popup returns you to where you were
rather than the first screen. What happens next depends on when it closed:

- **Before the countdown** — nothing has been typed into the device and nothing
  is committed, so the sequence simply runs again.
- **During the countdown or playback** — you land in an interrupted state.
  Restarting reads the passcode back from the cache, generates fresh decoy taps,
  and begins a new thirty-second countdown.
- **If that cache is gone** — exit setup and start it again.
- **After the passcode is typed but before you confirm** — the encrypted backup
  already exists; only the deadline is missing. The device stays **Pending** and
  can be resumed from your device list days later.

## Managing your devices

**List My Devices** shows every device you've set up that hasn't been deleted,
with the time remaining on each.

That remaining time is calculated on our server from the stored unlock time — not
from your computer's clock. Changing your system time, your time zone, or
travelling does not move an unlock date.

What you can do to a device depends on its status:

- **Pending** — setup was started but never confirmed. Resume it to finish, or
  start again.
- **Locked, time remaining** — you can **extend** the lock. You cannot shorten
  it. You can open it early only by spending a rescue pass, below.
- **Locked, time elapsed** — you can now **extend** it again, or mark it
  **Unlocked** and retrieve the passcode.
- **Unlocked** — the only status that can be marked **Deleted**.

Extending is always available because adding time is never something you'll
regret at 2am.

## Rescue passes

A lock you genuinely cannot open is a lock that eventually traps someone for a
real reason — a lost device, a family emergency, a mistake made while setting a
duration. So there is a way out, and it is deliberately a small one.

Every account gets **three rescue passes. Not three per device, not three per
month — three, ever.** Spending one opens a still-locked device and returns its
passcode.

They do not come back. There is no way to buy, earn, or reset them, and asking
us won't produce more — we haven't built the ability to grant any. When they're
gone, every remaining lock on the account runs to its own end.

You can also switch rescue off entirely for your account. That is **permanent**
— there is no way to switch it back on, by you or by us. If you want a lock with
no exit at all, that's the switch, and you should think about it before you touch
it rather than after.

A rescue pass is only spent on success. If a device's backup can't be read, or
the request fails partway, you keep the pass. Retrying a rescue that already went
through returns the same passcode and doesn't charge a second one.

## When the network is slow or gone

Every request is bounded: ten seconds for a read, twenty for a write. That
deadline covers the whole operation including the sign-in token refresh, not just
the network call — a stalled refresh happens *before* any request is sent, so a
timeout on the request alone would never fire and the popup would wait forever.

Failures are sorted into five kinds — offline, timeout, unreachable, server, and
request — and the popup uses the same words for the same failure on every screen.

**Retries are manual, and that's deliberate.** Chrome destroys the popup whenever
it loses focus, so a silent background retry usually dies unseen. You're right
there; one button press is more honest than a spinner that may already be dead.

Pressing retry is always safe. Every write that can be retried is replay-safe:
starting setup is keyed to the device, locking returns early if the device is
already locked, and extending carries an operation ID the server records, so a
retry claims the original operation instead of starting a second one. You cannot
accidentally extend a lock twice by pressing the button twice.

## What the extension can access

The extension requests exactly one Chrome permission: `storage`.

It does not request your tabs, your browsing history, your identity, Google
Drive, or access to your files. It cannot see what you browse, because it never
asks for the ability to.

Your passcode is encrypted and decrypted on our server, whose key is not shipped
inside the extension — pulling the extension apart doesn't reveal anyone's
passcode, including your own. Sensitive setup data is held in Chrome's session
storage, which is cleared when the browser closes; the only thing kept in
longer-term local storage is your email address, so you don't have to retype it.
