# yap

Minimal chat on your [Solid](https://solidproject.org) pod. One self-contained
HTML file, no build, signs in with the universal **xlogin** pill (Solid or Nostr).

`yap` is the **codename / test version** of the suite's chat. The real version
extends it into a Telegram-style desktop app with pod **and** nostr comms — built
in phases.

## v1 (this) — pod rooms

- A chat **room** is a single resource on a pod using the
  [Solid Chat](https://solid.github.io/chat/) data model: a `meeting:LongChat`
  with `flow:message` → `flow:Message` (`sioc:content`, `dct:created`,
  `foaf:maker`).
- Stored and read as **JSON-LD** via content negotiation
  (`Accept: application/ld+json`) — every Solid server speaks it, so there's no
  RDF/Turtle parser to ship. (Turtle interop with solid-chat/SolidOS is a later
  phase.)
- **Open** your room (defaults to `<pod>/public/yap.jsonld`, auto-created on first
  use), **post** messages, and the app **polls** every few seconds for new ones.
- Open any room by URL, or deep-link `?chat=<room-url>` (also accepts the suite's
  `url` intent) — share a link, anyone with read access sees it; posting needs
  write access to that resource.

## Nostr rooms — chat across your devices

A second room type for **live, cross-device** chat (e.g. your phone ↔ laptop ↔
desktop), no pod or login required:

- A room is a shared channel on a **nostr relay** (default `wss://melvin.me/relay`,
  editable via the **Device** button) keyed by a `#t` tag. Open one with
  `nostr:<name>` (e.g. `nostr:devices`) or the welcome-screen link.
- Each device holds its **own nostr key** (generated on first use, stored locally)
  with an editable **label** so you can tell devices apart. Messages are
  signed `kind:42` events; delivery is **live** over the relay's WebSocket — no
  polling.
- Point it at a **LAN relay** (`ws://…`) for fully-local chat — but note browsers
  block `ws://` from an `https://` page, so a plain-`ws://` LAN relay only works
  when yap is served over **http** (e.g. from your local jspod / solid-desktop);
  `wss://melvin.me` works from anywhere.

Purple, minimal, no theme switcher.

## Later phases

- Pod ↔ nostr mirroring (durable LongChat history + live nostr delivery in one
  room); message encryption (NIP-44/NIP-17) for private rooms.
- Real-time updates for pod rooms (WebSocket / `Updates-Via`) instead of polling.
- Reactions (`schema:ReactAction`), edit/delete, media, markdown, Type Index
  chat discovery, Turtle interop — then the desktop shell.

## Run

Static — open `index.html`, or install via the **store** to `/public/apps/yap/`.

AGPL-3.0-only.
