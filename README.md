# about-feed

Product list read by the Gley About window (`Tools/Gley/About`) that ships inside every Gley Unity asset.

The window downloads `v1/feed.json` from `raw.githubusercontent.com` each time it opens, and each product icon once. Nothing about the user or their project is sent. Offline, it shows the copy bundled in the package.

## Layout

- `v1/feed.json`: the feed.
- `v1/icons/<id>.png`: product icons, referenced by each product's `iconUrl`.

## Rules

1. **v1 is additive only.** Add fields, never rename, remove or change the meaning of one. Old About versions read this file for years. A breaking change goes in a new `v2/` folder, and `v1/` stays frozen.
2. **Set `updated` on every edit**, to the current UTC time. The window shows whichever of the downloaded cache and the bundled copy has the later `updated`.
3. **To change an icon, upload it under a new file name** (for example `traffic-system-v2.png`) and update `iconUrl`. Images are cached by URL forever, so replacing a file under the same name never reaches users who already have it.
4. **All dates are ISO 8601 UTC**, for example `2026-11-03T00:00:00Z`. An empty `start` means active now; an empty `end` means active until removed.
5. The shape must fit Unity's `JsonUtility`: no `null`, no maps, every object and array present. Use `""` for "none".
6. Before each About release, copy `v1/feed.json` to `Editor/Feed/AboutFeed.json` and `v1/icons/` to `Editor/Feed/Icons/` in the package.
