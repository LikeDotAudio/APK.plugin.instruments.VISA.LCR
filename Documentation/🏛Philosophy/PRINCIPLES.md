# Principles — INSTRUMENT.LCR

← [Philosophy](INDEX.md)

1. **One thing, one repository.** The LCR family is one bench thing: its models, its panel and its SDK travel together, and nothing about it lives in the parent except the folder's place (`families.json`) and its tab (`manifest.json`).
2. **The table is the source.** Each model's `<Model>.komand` is the command table; `<Model>.api.json` and the SDK pages are generated from it (`_komand/generate_device_apis.py`, `_komand/family_sdk_docs.py` in the parent) and checked, never hand-edited.
3. **No model is named in code.** Readers find models by listing this folder; the family's role on the bench is data, in `thing.json`.
4. **Unverified is said.** A command transcribed from a manual and never answered by an instrument carries `unverified` all the way to the SDK page.
