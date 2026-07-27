---
name: Look up public Highrise data
description: Read public Highrise users, rooms, posts, items and grabs via the read-only Web API.
api: openapi/highrise-web-api-openapi.yml
operations: [getUser, getUsers, getRoom, getRooms, getItem, getItems, getPost, getGrab]
---

# Look up public Highrise data

The Highrise Web API (`https://webapi.highrise.game`) is **read-only** JSON over HTTPS. No auth is
required for public data.

## Steps

1. **Fetch a single resource by id** — call `getUser` (`GET /users/{user_id}`), `getRoom`
   (`GET /rooms/{room_id}`), `getItem` (`GET /items/{item_id}`), `getPost` (`GET /posts/{post_id}`)
   or `getGrab` (`GET /grabs/{grab_id}`). A missing/private id returns `404`.
2. **List / search a collection** — call `getUsers`, `getRooms`, `getItems`, etc. Page with the
   cursor params from `conventions/highrise-conventions.yml`: `starts_after` (cursor), `sort_order`
   (`asc`/`desc`), and `limit`.
3. **Walk relationships** — a room's `owner` and a post's `author` are user ids; resolve them with
   `getUser`. See `data-model/highrise-data-model.yml`.

## Notes
- Ids are opaque strings.
- From a bot, the same data is available via the SDK's `self.webapi` helper.
