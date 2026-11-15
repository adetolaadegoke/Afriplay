# Afriplay API

All JSON API requests use the API origin (default `http://localhost:4000`). Authentication is an httpOnly `afriplay_session` cookie.

| Area | Endpoint | Purpose |
|---|---|---|
| Auth | `POST /auth/register`, `POST /auth/login`, `POST /auth/logout` | Accounts and sessions |
| Catalogue | `GET /songs`, `GET /songs/:id`, `GET /search?q=` | Approved public music and search |
| Library | `POST /playlists`, `GET /playlists/:id`, `POST/DELETE /playlists/:id/songs` | User playlists |
| Engagement | `POST/DELETE /songs/:id/favorite`, `POST /artists/:id/follow`, `POST /history` | Likes, follows, listening data |
| Artist | `POST /artist/songs` | Artist release submission (pending approval) |
| Admin | `GET /admin/dashboard`, `PATCH /admin/songs/:id/status` | Role-protected operations |
| Billing | `POST /payments/initialize`, `GET /payments/verify` | Server-side Paystack verification |

Every list endpoint is pagination-ready; `/songs` accepts `page` and `q`.
