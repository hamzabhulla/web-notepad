# API reference

All endpoints are Vercel serverless functions in `api/`. Sync requests send the sync key in an `x-sync-key` header.

| Method and path | Purpose | Authentication |
| --- | --- | --- |
| `GET /api/health` | Reports API and storage configuration and checks Redis connectivity | None |
| `GET /api/notes?meta=1` | Returns note metadata without note bodies | `x-sync-key` |
| `GET /api/notes?id=NOTE_ID` | Returns one note | `x-sync-key` |
| `GET /api/notes` | Returns the note collection | `x-sync-key` |
| `PUT /api/notes` | Creates or updates a note from a JSON body: `{ "note": { ... } }` | `x-sync-key` |

## Sync keys

A sync key must be 16 to 128 characters of letters, numbers, underscores, or hyphens. The app lowercases it and strips whitespace. The API hashes the key with SHA-256 to derive the storage namespace. Hashing identifies the namespace; note content is not end-to-end encrypted.

## Limits

- Up to 500 notes per sync key.
- Per-note size limits apply; very large notes (usually because of embedded images) are rejected with `note_too_large`. The documented limits are about 3,000,000 characters of note HTML and 500,000 characters of extra metadata.

## Error codes

These are the codes the app understands.

| Code | Meaning |
| --- | --- |
| `storage_not_configured` | Upstash Redis isn't connected to the Vercel project (or it wasn't redeployed) |
| `invalid_sync_key` | The key doesn't meet the format rules |
| `note_too_large` | One note exceeds the size limit |
| `too_many_notes` | The 500-note limit for the key was reached |
| `bad_note` | The note payload was rejected |
| `server_error` | Server or database error (may include a `detail` message) |

## Health check

`GET /api/health` needs no key. A deployment with sync fully set up reports storage as `configured` and Redis as `ok`. If it reports an error, see [Troubleshooting](TROUBLESHOOTING.md).

[Back to the README](../README.md)
