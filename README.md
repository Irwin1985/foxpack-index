# FoxPack index

The list of libraries that `foxpack add <name>` knows by name. FoxPack reads
`index.json` from this repository; the versions come from the tags of each
library's own repository.

```
foxpack add jsonfox
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
