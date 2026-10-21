# Troubleshooting

## Sync can't reach the server

1. In the app, open **Cloud sync** and click **Test connection**.
2. Visit `https://YOUR-DOMAIN/api/health` and look for storage `configured` and Redis `ok`.
3. Confirm Upstash is connected and the environment variables are set for the right Vercel environment, then redeploy.
4. Confirm both devices show the same **Key ID**.

## "The sync function (/api/notes) was not found"

Deploy the whole project, including the `api/` folder.

## Vercel blocks the app on a phone

Open the production domain instead of a protected preview URL, or change Deployment Protection for that deployment. If the connection test still fails, check for a VPN or ad blocker.

## A note won't sync

Check the [limits](API.md#limits) and remove large embedded images. **Test connection** helps tell a service problem from a note-size problem.

## Notes seem to be missing

- For local-only notes, check the original browser profile; notes don't move between browsers on their own.
- For synced notes, confirm the same Key ID is active on both devices.
- Before clearing site data, make sure you have a recent JSON backup (**Backup all**).
- If you see "Browser storage is full", download your notes and remove large images.

[Back to the README](../README.md)
