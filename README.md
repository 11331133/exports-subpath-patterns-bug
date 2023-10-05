Steps to reproduce:

1. Make sure everything works:

```
yarn
yarn workspace lib1 build
yarn workspace app1 build
node app1/dist/app.js
```

2. Change `exports` in `libs/lib1/package.json`:
```diff
-       "./": "./dist/"
+       "./*": "./dist/*"
``` 
3. Run:
```
node app1/dist/app.js
```
4. See the following error:
```
Error: Cannot find module '/exports-subpath-patterns-bug/node_modules/lib1/dist/folder1'
    at createEsmNotFoundErr (node:internal/modules/cjs/loader:1055:15)
    at finalizeEsmResolution (node:internal/modules/cjs/loader:1048:15)
    at resolveExports (node:internal/modules/cjs/loader:556:14)
    at Function.Module._findPath (node:internal/modules/cjs/loader:596:31)
    at Function.Module._resolveFilename (node:internal/modules/cjs/loader:1014:27)
    at Function.Module._load (node:internal/modules/cjs/loader:873:27)
    at Module.require (node:internal/modules/cjs/loader:1100:19)
    at require (node:internal/modules/cjs/helpers:119:18)
    at Object.<anonymous> (/exports-subpath-patterns-bug/app1/dist/app.js:3:19)
    at Module._compile (node:internal/modules/cjs/loader:1198:14) {
  code: 'MODULE_NOT_FOUND',
  path: '/exports-subpath-patterns-bug/node_modules/lib1/package.json'

```