# New platform

## Dev setup

## Running code

```sh
# all commands from the root directory
yarn kbn bootstrap
yarn kbn run build --skip-kibana --skip-kibana-extra
```

If you get into a weird state you might clean the `target` directories,
`yarn kbn clean`.

When this completes you can start the server and plugins as a standalone Node application:

```bash
node scripts/platform.js
```

Or load it as a part of the legacy platform:

```bash
yarn start
```

In the latter case, all Kibana requests will hit the new platform first and it will decide whether request can be
solely handled by the new platform or request should be forwarded to the legacy platform. In this mode new platform does
not read config file directly, but rather transforms config provided by the legacy platform. In addition to that all log
records are forwarded to the legacy platform so that it can layout and output them properly.

## Running tests

Run Jest:

```
node scripts/jest.js
```

(add `--watch` for re-running on change)

## VSCode

If you want to see what it looks like with fantastic editor support.

```
$ cat ~/.vscode/settings.json
// Place your settings in this file to overwrite default and user settings.
{
  "typescript.tsdk": "./node_modules/typescript/lib",
  "typescript.referencesCodeLens.enabled": true
}
```

## Starting plugins in the new platform

Plugins in `../core_plugins` will be started automatically. In addition, dirs to
scan for plugins can be specified in the Kibana config by setting the
`__newPlatform.plugins.scanDirs` value, e.g.

```yaml
__newPlatform:
  plugins:
    scanDirs: ['./example_plugins']
```