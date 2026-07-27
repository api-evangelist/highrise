---
name: Run a bot inside a Highrise room
description: Connect a bot to a Highrise room over the Bot API WebSocket, handle room events, and respond.
api: asyncapi/highrise-bot-api-asyncapi.yml
operations: [onChat, onUserJoined, onTipReaction]
---

# Run a bot inside a Highrise room

Highrise bots run over a WebSocket at `wss://highrise.game/web/botapi`. The official
`highrise-bot-sdk` (Python) handles the connection.

## Setup

1. **Get credentials** — mint an API token in Highrise account settings
   (`https://highrise.game/account/settings`, "Bots & API Keys") and copy the target **room id**
   from the room's share link. See `authentication/highrise-authentication.yml`.
2. **Install** — `pip install highrise-bot-sdk` (`packages/highrise-packages.yml`).

## Build the bot

3. **Extend `BaseBot`** and override event handlers. Map to the AsyncAPI channels in
   `asyncapi/highrise-bot-api-asyncapi.yml`:
   - `onChat` (`on_message`) — react to chat.
   - `onUserJoined` (`on_user_join`) — greet arrivals, e.g. teleport or send a welcome chat.
   - `onTipReaction` — acknowledge tips.
4. **Act** — issue Bot API requests: send a chat message, teleport a user, moderate the room, tip a
   user, manage the bot's backpack/outfit, or send a DM. Requests are correlated to responses by a
   client `rid` (`conventions/highrise-conventions.yml`); errors arrive as an `Error` message
   (`errors/highrise-problem-types.yml`).

## Run

5. `highrise mybot:Bot <room_id> <api_token>` (see `cli/highrise-cli.yml`). Subscribe to a subset of
   events with the `?events=chat,user_joined` connection query parameter.
