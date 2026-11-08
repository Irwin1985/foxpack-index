# FoxPack index

The list of libraries that `foxpack add <name>` knows by name, and of the FoxDock
plugins that `foxpack plugin add <id>` knows. FoxPack reads `index.json` from this
repository; the versions come from the tags of each library's or plugin's own
repository.

```
foxpack add jsonfox
foxpack plugin add history
```

## Adding a library

1. Put a `foxpack.json` in the root of your repository:

   ```json
   {
     "name": "mylib",
     "version": "1.0",
     "description": "What it does",
     "license": "MIT",
     "files": ["MyLib.prg"],
     "usage": "loLib = NEWOBJECT(\"MyLib\", \"MyLib.prg\")"
   }
   ```

2. Tag the commit with the same version: `v1.0`.
3. Open a pull request here that adds an entry to `index.json`.

A library that is not in the index can still be installed with
`foxpack add github:user/repo`, after confirming it.

## Adding a FoxDock plugin

1. Put a `foxpack.json` in the root of your repository, with `kind`, `id` and
   `foxdockApi`:

   ```json
   {
     "name": "foxdock-history",
     "kind": "foxdock-plugin",
     "id": "history",
     "foxdockApi": 1,
     "version": "1.0.0",
     "description": "The IDE's command history",
     "license": "MIT",
     "files": ["HistoryPlugin.prg", "HistoryStrings.prg"],
     "requires": ["jsonfox@13.2.0"]
   }
   ```

   `HistoryPlugin.prg` (the id with `Plugin.prg` after it) must be at the root. The
   [FoxPack README](https://github.com/Irwin1985/FoxPack#foxdock-plugins) has the
   rules of each field.

2. Tag the commit with the same version: `v1.0.0`.
3. Open a pull request here that adds an entry to `index.json`, with the same
   `kind` and `id`:

   ```json
   {
     "name": "foxdock-history",
     "kind": "foxdock-plugin",
     "id": "history",
     "repo": "you/foxdock-history",
     "description": "The IDE's command history"
   }
   ```

A plugin that is not in the index can still be installed with
`foxpack plugin add github:user/repo`, after confirming it. FoxDock shows it as
unreviewed.

## The fields of an entry

| Field | Rule |
|---|---|
| `name` | Required, and unique in the whole index, libraries and plugins together. It must be the `name` of the repository's `foxpack.json` |
| `repo` | Required: `user/repo` on GitHub |
| `description` | One line, shown by `foxpack plugin available` and in FoxDock |
| `kind` | `library` when it is missing, or `foxdock-plugin` |
| `id` | Required in a plugin, and unique among the plugins: lowercase letters, digits and `_`, starting with a letter, up to 30 characters. It must be the `id` of the repository's `foxpack.json` |
| `house` | `true` for the libraries and plugins of the house; `false` when it is missing |

An entry that breaks a rule (a `kind` FoxPack does not know, a plugin without a
valid `id`, an `id` or a `name` that another entry already has) is skipped, so
the rest of the index keeps working.
