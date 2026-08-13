---
title: "Why the passcode is one you never see"
description: >-
  Every blocker fails the same way: the person who installed it is the person
  who can remove it. Here's the one design decision that changes that.
date: 2026-08-14
---

Every content blocker has the same hole in it, and it isn't technical. The
person who installs the blocker is the person who can remove it. Whatever
willpower put it there has to still be present, in full, at the exact moment it
is weakest. That is the one moment it never is.

So the useful question isn't "how do we block this well." iOS already blocks it
well — Screen Time's content restrictions are built into the operating system and
have been for years. The useful question is: **how does a decision you make today
survive contact with the person you'll be at 2am on a Thursday?**

## Move the decision, not the enforcement

The answer we landed on is that the passcode should never exist in your head.

When you set a device up, the extension generates a random Screen Time passcode.
Before it shows you anything at all, it sends that passcode to our server, which
encrypts it and files it under your account. Only then does a thirty-second
countdown begin, and the digits are played to you one keypad tap at a time,
mixed with decoy taps, while you follow along on the phone.

Thirty seconds later the restrictions are on, and the passcode exists in exactly
one place: encrypted, on a server, behind a clock.

You didn't memorise it, because you were never shown it as a number. You can't
look it up, because the decryption key isn't in the extension — taking the
extension apart gets you nothing. And you can't simply ask for it back, because
the only thing standing between you and it is the number of days you chose while
you still wanted the block to work.

## The clock starts when the lock does

One detail took longer to get right than the encryption did: when the countdown
starts.

The obvious implementation sets the deadline when setup begins. It's also wrong.
Setup can be abandoned halfway — you get interrupted, you close the tab, Chrome
destroys the popup because it lost focus. Come back four days later and finish,
and a deadline set at the start has quietly eaten four days you spent completely
unlocked.

So the duration isn't even asked for until the end. You confirm, and the unlock
time is written once, at that instant, and never rewritten. A device you set up
but never confirmed sits as *Pending* and can be finished next week with the full
term still ahead of it.

## Extending is easy on purpose

You can always add time to a lock. You can never take it away.

That asymmetry is the whole product. Adding time is not a decision anyone regrets
at 2am — nobody's worst moment involves an urge to be *more* restricted. Removing
time is the only thing a blocker has to defend against, and a lock you can
shorten is a lock that stops working precisely when it was supposed to start.

Once the days are up, the lock opens. Not before. That isn't a limitation we
haven't got around to fixing — it's the feature, and everything else is
plumbing.
