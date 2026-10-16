# ePy Studio - install artifacts

Author: Ing. Angel Navarro-Mora M.Sc.

**One repository carries every executable ePy Studio's installer needs.**
Nothing else in the suite commits a binary or disperses them across repos: a
build stages its output here, and `epy_studio/windows/epy_studio.iss` is what
turns it into an install.

## What is here, and why one place

Two kinds of artifact reach the user through ePy Studio:

* the **editor apps** Studio's own PyInstaller build produces
  (`epy_reports.exe`, `epy_slides.exe`, `epy_papers.exe`, ...), and
* the **adopted Crafting Apps** - the ePy family's copies of ArtCraft's
  pure-Rust tools, renamed with the `epy_` prefix (`epy_cadcraft` and the
  rest). Studio never builds them; its installer copies them.

Keeping them in a single repository is deliberate. The installer consumes ONE
tree, and an adopted tool is a foreign program redistributed WITH the bundle,
so its provenance is recorded in `manifest.epyson` (the same `upstream` the
Studio catalog carries).

## Layout

```
apps/<id>/<id>.exe          the editor apps (id = epy_reports, ...)
apps/_internal/             the shared runtime the apps need
crafts/<binary>/            an adopted tool, under its UPSTREAM stem
  <binary>.exe              (cadcraft.exe ..., NOT epy_cadcraft.exe)
  <binary>-cli.exe          its batch/MCP CLI, read by the drawing flow
```

`manifest.epyson` lists exactly what a complete bundle must carry; it is
generated from `epy_studio/src/epy_studio/_config/apps.epyson`, so the two
cannot drift.

## How it reaches an install

`epy_studio/build.py` stages a build under `dist/epy_studio/`, and the Inno
script (`windows/epy_studio.iss`) copies it per component. An adopted craft
lands at `{app}\crafts\<binary>\`, **guarded with `#ifexist`** so the
installer compiles whether or not the binary was staged. ePy Studio then finds
it through `installed_exe` (`install_dir()/crafts/<binary>/`), and hands its
CLI to the applications it launches through `craft_env` (`EPY_<BINARY>_CLI`).

## Licence

The editor apps are this suite's own. The adopted crafts are MIT OR
Apache-2.0 clean-room reimplementations of Adobe / Microsoft / Autodesk tools
(`github.com/storytold`), copied here with their notices; the non-OSI ones
(`artcraft`, `artcraft-services`, `artcraftx`) are NOT redistributed. See
`manifest.epyson`'s `upstream` field per craft.
