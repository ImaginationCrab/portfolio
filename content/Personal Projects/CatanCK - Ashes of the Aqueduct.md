---
title: CatanCK - Ashes of the Aqueduct
description: A multiplayer Cities & Knights implementation with a Python rules engine and a Unity 3D client.
tags:
  - project
  - multiplayer
  - python
  - unity
  - distributed-systems
status: in-progress
repo: Private Repo, request access with me directly
draft: false
---

# CatanCK - Ashes of the Aqueduct

A from-scratch multiplayer implementation of **Settlers of Catan: Cities & Knights** — the expansion nobody wants to implement, because the rule interactions are genuinely nasty. Barbarian tracks, progress card decks, knight activation/promotion, city walls, the metropolis race, and the way all of those quietly modify the base game's turn structure.

The goal was never "clone a board game." It was to build an authoritative game server where the rules engine is the source of truth, clients are dumb renderers, and the whole thing survives real players on a real network.

> [!note] Status
> Playable end to end. Actively being restructured — see [Where it's going](#where-its-going).

## Architecture

```
Unity URP client  ──WebSocket──>  Cloudflare Tunnel  ──>  FastAPI server (Oracle Cloud ARM)
                                                              │
                                                              └── authoritative game engine
```

**Server — Python / FastAPI.** The rules engine is pure and deterministic: it takes a game state plus an action and returns a new state or a rejection. No I/O, no framework coupling, no rendering concerns. Every legality check lives here, so a modified client can't do anything the server won't independently agree to.

**Transport — WebSockets.** Rooms hold connected players, broadcast state deltas, and handle the reconnect case, which matters more than it sounds like it does in a game that runs 90+ minutes.

**Hosting — Oracle Cloud ARM VM behind a Cloudflare Tunnel.** The tunnel means no inbound ports on the VM and no origin IP to find; Cloudflare terminates TLS and handles the public hostname. Free-tier ARM instances are generous enough to be a legitimate deploy target rather than a compromise.

**Client — Unity, URP.** 3D board with hex tile generation, vertex/edge placement snapping, and a UI layer driven entirely by server state. The client never decides anything; it asks and renders the answer.

## Things that were harder than expected

**Cities & Knights turn structure.** The base game's turn is roughly *roll → trade → build*. C&K injects the barbarian advance, the event die, progress card draws, aqueduct handling, and knight actions that can be taken in the middle of other players' turns. Modeling this as a clean state machine — rather than a pile of conditionals — took several rewrites.

**Partial information.** Hands are hidden, progress cards are hidden, and the server has to enforce that without ever shipping the full state to a client that shouldn't see it. Every broadcast is filtered per-recipient.

**Authoritative-but-responsive.** Waiting on a round trip for every UI interaction feels awful. The client optimistically previews placements it's fairly sure are legal, and reconciles when the server answers.

## Where it's going

Currently spec'd out, not yet built:

- **Cloudflare Durable Objects for room state.** Each game room becomes a single-threaded stateful object at the edge, which eliminates the "one VM holds all rooms" scaling ceiling and gives per-room consistency for free.
- **WebSocket authentication via ticket exchange.** Browsers can't set custom `Authorization` headers on WebSocket connections, so auth happens over HTTP first and returns a short-lived single-use ticket that the socket handshake presents.
- **A 2D SVG web client.** Unity is a heavy ask for "click a link and play." An SVG board with an anonymous account system lowers the barrier to a shared URL.
- **A TypeScript port of the engine**, validated against the Python original with differential testing — same action sequences, both engines, assert identical states. Necessary if the engine is going to run inside a Durable Object.

## Stack

`Python` · `FastAPI` · `WebSockets` · `Unity (URP)` · `C#` · `Cloudflare Tunnel` · `Oracle Cloud`


## Why?

My friends and I play a large amount of this expansion, to the point where we wanted to implement our own home rules. These rules rebalance the game, making the game much more fair for all play-styles, hence the name "Ashes of the Aqueduct". I implemented our rules into the game, making it an experience that doesn't anywhere else in the world.