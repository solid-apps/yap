# yap

Chat on your [Solid](https://solidproject.org) pod. One self-contained HTML file,
no build, signs in with the universal **xlogin** pill.

`yap` is the **chat suite** for the solid-apps ecosystem, built in phases toward a
Telegram-style messenger over pod **and** nostr.

## This phase — encrypted DMs

A two-pane messenger for **1:1 encrypted direct messages**:

- **Roster** (left): your conversations — contacts (`kind:3` follows) plus anyone
  you've exchanged messages with — newest first, with avatar, last-message
  preview, timestamps, and **unread badges** (read state saved to your pod at
  `/private/yap/read.jsonld`).
- **Thread** (right): a live chat. Messages are **NIP-04** encrypted (`kind:4`),
  signed with your **WebID identity key** (read from the shared keystore at
  `/private/nostr/keys.jsonld` — *one key, every app*), published to your relays,
  and delivered **live** over a standing subscription.
- **LAN-only toggle** (`🌐 → 🔒`): route a conversation over **your pod's relay +
  the contact's relay** only, so it never touches a public relay. (Plain `ws://`
  LAN relays only work when yap is served over **http**, e.g. your local jspod.)
- **+ New**: start a chat from an `npub`, hex pubkey, or a WebID / pod URL
  (resolves the key from their card's `verificationMethod`).

Identity, keys, follows, and relays are managed in the **nostr** app; yap reads
the same keystore so it's the same you everywhere.

## Earlier (returning in a later phase)

Pod rooms ([Solid Chat](https://solid.github.io/chat/) `meeting:LongChat` JSON-LD)
and live nostr **group** rooms (`kind:42`, per-device keys) shipped in the
previous version. They're temporarily set aside while the DM shell lands, and
fold back into the roster next.

## Later phases

- Group rooms (pod + nostr) back in the unified roster
- **NIP-17** gift-wrapped DMs (hide the `p`-tag / metadata)
- Pod ↔ nostr mirroring (durable history + live delivery), reactions, media,
  markdown, Type Index chat discovery

## Run

Static — open `index.html`, or install via the **store** to `/public/apps/yap/`.
Needs a Nostr identity (set one up in the **nostr** app) to send DMs.

AGPL-3.0-only.
