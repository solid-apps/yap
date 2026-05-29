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

Purple, minimal, no theme switcher.

## Later phases

- Real-time updates (WebSocket / `Updates-Via`) instead of polling.
- **Nostr** transport for cross-pod / offline-pod delivery (sidesteps the
  localhost reachability ceiling).
- Reactions (`schema:ReactAction`), edit/delete, media, markdown, Type Index
  chat discovery, themes — then the desktop shell.

## Run

Static — open `index.html`, or install via the **store** to `/public/apps/yap/`.

AGPL-3.0-only.
