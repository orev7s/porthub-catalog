# PortHub Catalog

The public feed behind [PortHub](https://github.com/orev7s/porthub) — one JSON file listing
Android game ports, decompilations, recompilations and engine reimplementations.

```
https://raw.githubusercontent.com/orev7s/porthub-catalog/main/games.json
```

- **1239 entries**, every one a pointer: repo, releases, APK link, artwork, status.
- **No game data.** No ROMs, ISOs, assets or repackaged APKs. APK links point at the
  project's own release page.
- Schema: [`schema/game.schema.json`](schema/game.schema.json).

## What a record looks like

```json
{
  "id": "banjo-kazooie-recomp",
  "title": "Banjo-Kazooie Recomp",
  "originalTitle": "Banjo-Kazooie",
  "portType": "recompilation",
  "status": "stable",
  "android": { "supported": true, "minAndroid": "8.0", "abis": ["arm64-v8a"], "requiresGameFiles": "owned" },
  "artwork": { "cover": "https://…/library_600x900.jpg", "accent": "#6C7BFF" },
  "links": { "repo": "https://github.com/…", "releases": "https://github.com/…/releases" },
  "downloads": [{ "label": "Latest APK", "kind": "apk", "url": "https://github.com/…/releases/latest" }],
  "sources": ["droid-recomp"]
}
```

One game may appear several times — different implementations, different repos. That is
deliberate: the app shows each implementation separately so you can pick the one that
actually runs on your device.

## Sources and attribution

| Source | Licence | Used for |
|---|---|---|
| [Kymie131/openportsgames](https://github.com/Kymie131/openportsgames) | data CC BY 4.0 | year, publisher, genre, summary, covers |
| [MooPuu/droid-recomp](https://github.com/MooPuu/droid-recomp) | MIT | Android packages, min Android, ABIs, APK links |
| [Nyaldee/Ports-Launcher](https://github.com/Nyaldee/Ports-Launcher) | see repo | Android package ids, SteamGridDB art, install notes |
| [abduznik/awesome-android-native-ports](https://github.com/abduznik/awesome-android-native-ports) | see repo | breadth of source ports |
| [abduznik/awesome-x360-recomps](https://github.com/abduznik/awesome-x360-recomps) | see repo | Xbox 360 recompilations |
| [yibie/awesome-rea](https://github.com/yibie/awesome-rea) | see repo | decompilation / RE research |

Entries derived from OpenPortsGames data are CC BY 4.0; attribution is kept in each
record's `sources` array. Each port keeps its own upstream licence in `license`.

## Rebuilding

```bash
git clone --depth 1 https://github.com/Kymie131/openportsgames feedsrc/Kymie131_openportsgames
# …plus the other sources
python3 tools/import_sources.py --src feedsrc -o games.json
```

Takedown requests: open an issue here, or contact the repo that actually hosts the port.
This catalog only links.
