# ePy Studio - the PUBLIC executables

Author: Ing. Angel Navarro-Mora M.Sc.

**Every PUBLIC ePy Studio executable is downloaded from this ONE public
repository.** The private ones live in `estructuraPy/epy_studio_install_private`
and are never copied here: a public deployment reads one URL, an internal
one reads another.

## What is here

- the public editors Studio builds (`epy_reports`, `epy_slides`, `epy_papers`);
- the adopted ArtCraft Crafting Apps (MIT OR Apache-2.0);
- the PUBLIC installer, built without the private editors.

## Layout

```
apps/<id>/<id>.exe          the editor apps
crafts/<binary>/            an adopted tool, under its UPSTREAM stem
  <binary>.exe              (cadcraft.exe ..., never epy_cadcraft.exe)
  <binary>-cli.exe          its batch/MCP CLI, read by the drawing flow
releases                    the installer built from these executables
```

`manifest.epyson` lists exactly what this site carries; it is generated from
`epy_studio/src/epy_studio/_config/apps.epyson`, so the two cannot drift.

## Licence

The editor apps are this suite's own. The adopted crafts are MIT OR
Apache-2.0 clean-room reimplementations of Adobe / Microsoft / Autodesk tools
(`github.com/storytold`); their `upstream` is recorded in `manifest.epyson`.
The non-OSI projects (`artcraft`, `artcraft-services`, `artcraftx`) are not
distributed.
