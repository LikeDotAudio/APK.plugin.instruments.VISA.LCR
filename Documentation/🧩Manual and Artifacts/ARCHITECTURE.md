# Architecture — INSTRUMENT.LCR

← [Manual and Artifacts](INDEX.md)

- `thing.json` — what the thing is on the bench (inputs / metering / monitoring / source) and where its inputs come from. Authored.
- `gui/` — the family panel. The orchestrator on the thick node stamps it once per discovered box and presents it retained at `APK.audio/System/Gui/Panels/<key>`; the OS Instruments tab and the Touch Panel Builder (`EDITORS.TouchPanelBuilder`, its `run.html` runs it live) both start from that.
- `<Model>/` — `<Model>.komand` (command table), `<Model>.gui`, `<Model>.api.json` (generated: verbs, routes, sockets, MQTT), `commands_tree.md`, `SOURCES.md`.
- `Documentation/🧩Manual and Artifacts/SDK.md` and `SDK/<Model>.md` — generated from the api.json files.

The family is read in place, by path, from the parent `INSTRUMENTS` checkout: the images that bake `INSTRUMENTS` (NODE.BareMetal, DISCOVERY.Engine, WEB.OsApi) copy the working tree, submodules included.
