# Grey Street ChatGPT Plugin Backend

This package turns the public **Grey Street** DMB live-history archive into a read-only MCP server for ChatGPT plugins.

Public app: https://davematthewsbandcompanion.netlify.app/

## Included tools

- `search_shows` — search 1991–2000 shows by year/date/venue/city/song/cover/guest/text.
- `get_show` — full show record, local setlist (when populated), covers, guests, sources and exact Almanac URL.
- `search_songs` — search locally populated song performances.
- `search_covers` — cover-title/original-artist search.
- `search_guests` — documented guests attached to local show records.
- `search_videos` — curated YouTube video records.
- `list_musicians` — musician/collaborator directory.
- `get_archive_stats` — archive coverage totals.

All tools are **read-only**. The server contains no private user data and performs no write actions.

## Deploy on Netlify

This needs a normal Netlify build because it contains a serverless Function. The simplest durable setup is a Git-backed Netlify project:

1. Put the contents of this folder in a GitHub repository.
2. In Netlify choose **Add new project → Import an existing project → GitHub**.
3. Select the repository. Netlify will detect `netlify.toml`.
4. Build command: leave blank. Publish directory: `public`.
5. Deploy.
6. Your MCP endpoint will be:
   `https://YOUR-PLUGIN-SITE.netlify.app/mcp`

Keep the finished Grey Street web app at its current URL. This MCP service can be deployed as a second Netlify site so there is no risk of breaking the app.

## Connect to ChatGPT

After the Netlify deploy succeeds:

1. Open **ChatGPT → Plugins**.
2. Select **+ → Create custom MCP server**.
3. Name it **Grey Street**.
4. Server URL: `https://YOUR-PLUGIN-SITE.netlify.app/mcp`
5. Authentication: **No authentication** (the archive is public and read-only).
6. Create the plugin, install it, and test it in a new chat/Work surface where plugins are available.

Good test prompts:

- `@Grey Street Find the DMB shows at Trax in 1992.`
- `@Grey Street Find locally indexed performances of Warehouse in 1991.`
- `@Grey Street What exact Almanac link do you have for the 1998-12-03 show?`
- `@Grey Street How many 1995 shows and exact links are indexed?`

## Important data boundary

Grey Street currently indexes 1,194 shows and 1,190 verified exact DMBAlmanac links. Only locally populated setlists should be treated as known song lists. Missing local setlist data is preserved as unknown rather than guessed.
