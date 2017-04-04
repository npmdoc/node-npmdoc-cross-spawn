# api documentation for  [cross-spawn (v5.1.0)](https://github.com/IndigoUnited/node-cross-spawn#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-cross-spawn.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-cross-spawn) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-cross-spawn.svg)](https://travis-ci.org/npmdoc/node-npmdoc-cross-spawn)
#### Cross platform child_process#spawn and child_process#spawnSync

[![NPM](https://nodei.co/npm/cross-spawn.png?downloads=true)](https://www.npmjs.com/package/cross-spawn)

[![apidoc](https://npmdoc.github.io/node-npmdoc-cross-spawn/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-cross-spawn_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-cross-spawn/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-cross-spawn/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-cross-spawn/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "IndigoUnited",
        "email": "hello@indigounited.com",
        "url": "http://indigounited.com"
    },
    "bugs": {
        "url": "https://github.com/IndigoUnited/node-cross-spawn/issues/"
    },
    "dependencies": {
        "lru-cache": "^4.0.1",
        "shebang-command": "^1.2.0",
        "which": "^1.2.9"
    },
    "description": "Cross platform child_process#spawn and child_process#spawnSync",
    "devDependencies": {
        "@satazor/eslint-config": "^3.0.0",
        "eslint": "^3.0.0",
        "expect.js": "^0.3.0",
        "glob": "^7.0.0",
        "mkdirp": "^0.5.1",
        "mocha": "^3.0.2",
        "once": "^1.4.0",
        "rimraf": "^2.5.0"
    },
    "directories": {},
    "dist": {
        "shasum": "e8bd0efee58fcff6f8f94510a0a554bbfa235449",
        "tarball": "https://registry.npmjs.org/cross-spawn/-/cross-spawn-5.1.0.tgz"
    },
    "files": [
        "index.js",
        "lib"
    ],
    "gitHead": "1da4c09ccf658079849a3d191b16e59bc600e8b4",
    "homepage": "https://github.com/IndigoUnited/node-cross-spawn#readme",
    "keywords": [
        "spawn",
        "spawnSync",
        "windows",
        "cross",
        "platform",
        "path",
        "ext",
        "path-ext",
        "path_ext",
        "shebang",
        "hashbang",
        "cmd",
        "execute"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "satazor",
            "email": "andremiguelcruz@msn.com"
        }
    ],
    "name": "cross-spawn",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/IndigoUnited/node-cross-spawn.git"
    },
    "scripts": {
        "lint": "eslint '{*.js,lib/**/*.js,test/**/*.js}'",
        "test": "node test/prepare && mocha --bail test/test"
    },
    "version": "5.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module cross-spawn](#apidoc.module.cross-spawn)
1.  [function <span class="apidocSignatureSpan">cross-spawn.</span>_parse (command, args, options)](#apidoc.element.cross-spawn._parse)
1.  [function <span class="apidocSignatureSpan">cross-spawn.</span>spawn (command, args, options)](#apidoc.element.cross-spawn.spawn)
1.  [function <span class="apidocSignatureSpan">cross-spawn.</span>sync (command, args, options)](#apidoc.element.cross-spawn.sync)
1.  object <span class="apidocSignatureSpan">cross-spawn.</span>_enoent

#### [module cross-spawn._enoent](#apidoc.module.cross-spawn._enoent)
1.  [function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>hookChildProcess (cp, parsed)](#apidoc.element.cross-spawn._enoent.hookChildProcess)
1.  [function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>notFoundError (command, syscall)](#apidoc.element.cross-spawn._enoent.notFoundError)
1.  [function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>verifyENOENT (status, parsed)](#apidoc.element.cross-spawn._enoent.verifyENOENT)
1.  [function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>verifyENOENTSync (status, parsed)](#apidoc.element.cross-spawn._enoent.verifyENOENTSync)



# <a name="apidoc.module.cross-spawn"></a>[module cross-spawn](#apidoc.module.cross-spawn)

#### <a name="apidoc.element.cross-spawn._parse"></a>[function <span class="apidocSignatureSpan">cross-spawn.</span>_parse (command, args, options)](#apidoc.element.cross-spawn._parse)
- description and source-code
```javascript
function parse(command, args, options) {
    var parsed;

    // Normalize arguments, similar to nodejs
    if (args && !Array.isArray(args)) {
        options = args;
        args = null;
    }

    args = args ? args.slice(0) : [];  // Clone array to avoid changing the original
    options = options || {};

    // Build our parsed object
    parsed = {
        command: command,
        args: args,
        options: options,
        file: undefined,
        original: command,
    };

    // Delegate further parsing to shell or non-shell
    return options.shell ? parseShell(parsed) : parseNonShell(parsed);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cross-spawn.spawn"></a>[function <span class="apidocSignatureSpan">cross-spawn.</span>spawn (command, args, options)](#apidoc.element.cross-spawn.spawn)
- description and source-code
```javascript
function spawn(command, args, options) {
    var parsed;
    var spawned;

    // Parse the arguments
    parsed = parse(command, args, options);

    // Spawn the child process
    spawned = cp.spawn(parsed.command, parsed.args, parsed.options);

    // Hook into child process "exit" event to emit an error if the command
    // does not exists, see: https://github.com/IndigoUnited/node-cross-spawn/issues/16
    enoent.hookChildProcess(spawned, parsed);

    return spawned;
}
```
- example usage
```shell
...
    var parsed;
    var spawned;

    // Parse the arguments
    parsed = parse(command, args, options);

    // Spawn the child process
    spawned = cp.spawn(parsed.command, parsed.args, parsed.options);

    // Hook into child process "exit" event to emit an error if the command
    // does not exists, see: https://github.com/IndigoUnited/node-cross-spawn/issues/16
    enoent.hookChildProcess(spawned, parsed);

    return spawned;
}
...
```

#### <a name="apidoc.element.cross-spawn.sync"></a>[function <span class="apidocSignatureSpan">cross-spawn.</span>sync (command, args, options)](#apidoc.element.cross-spawn.sync)
- description and source-code
```javascript
function spawnSync(command, args, options) {
    var parsed;
    var result;

    if (!cpSpawnSync) {
        try {
            cpSpawnSync = require('spawn-sync');  // eslint-disable-line global-require
        } catch (ex) {
            throw new Error(
                'In order to use spawnSync on node 0.10 or older, you must ' +
                'install spawn-sync:\n\n' +
                '  npm install spawn-sync --save'
            );
        }
    }

    // Parse the arguments
    parsed = parse(command, args, options);

    // Spawn the child process
    result = cpSpawnSync(parsed.command, parsed.args, parsed.options);

    // Analyze if the command does not exists, see: https://github.com/IndigoUnited/node-cross-spawn/issues/16
    result.error = result.error || enoent.verifyENOENTSync(result.status, parsed);

    return result;
}
```
- example usage
```shell
...
'''js
var spawn = require('cross-spawn');

// Spawn NPM asynchronously
var child = spawn('npm', ['list', '-g', '-depth', '0'], { stdio: 'inherit' });

// Spawn NPM synchronously
var results = spawn.sync('npm', ['list', '-g', '-depth', '0'], { stdio: 'inherit' });
'''


## Caveats

#### 'options.shell' as an alternative to 'cross-spawn'
...
```



# <a name="apidoc.module.cross-spawn._enoent"></a>[module cross-spawn._enoent](#apidoc.module.cross-spawn._enoent)

#### <a name="apidoc.element.cross-spawn._enoent.hookChildProcess"></a>[function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>hookChildProcess (cp, parsed)](#apidoc.element.cross-spawn._enoent.hookChildProcess)
- description and source-code
```javascript
function hookChildProcess(cp, parsed) {
    var originalEmit;

    if (!isWin) {
        return;
    }

    originalEmit = cp.emit;
    cp.emit = function (name, arg1) {
        var err;

        // If emitting "exit" event and exit code is 1, we need to check if
        // the command exists and emit an "error" instead
        // See: https://github.com/IndigoUnited/node-cross-spawn/issues/16
        if (name === 'exit') {
            err = verifyENOENT(arg1, parsed, 'spawn');

            if (err) {
                return originalEmit.call(cp, 'error', err);
            }
        }

        return originalEmit.apply(cp, arguments);
    };
}
```
- example usage
```shell
...
parsed = parse(command, args, options);

// Spawn the child process
spawned = cp.spawn(parsed.command, parsed.args, parsed.options);

// Hook into child process "exit" event to emit an error if the command
// does not exists, see: https://github.com/IndigoUnited/node-cross-spawn/issues/16
enoent.hookChildProcess(spawned, parsed);

return spawned;
}

function spawnSync(command, args, options) {
var parsed;
var result;
...
```

#### <a name="apidoc.element.cross-spawn._enoent.notFoundError"></a>[function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>notFoundError (command, syscall)](#apidoc.element.cross-spawn._enoent.notFoundError)
- description and source-code
```javascript
function notFoundError(command, syscall) {
    var err;

    err = new Error(syscall + ' ' + command + ' ENOENT');
    err.code = err.errno = 'ENOENT';
    err.syscall = syscall + ' ' + command;

    return err;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cross-spawn._enoent.verifyENOENT"></a>[function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>verifyENOENT (status, parsed)](#apidoc.element.cross-spawn._enoent.verifyENOENT)
- description and source-code
```javascript
function verifyENOENT(status, parsed) {
    if (isWin && status === 1 && !parsed.file) {
        return notFoundError(parsed.original, 'spawn');
    }

    return null;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cross-spawn._enoent.verifyENOENTSync"></a>[function <span class="apidocSignatureSpan">cross-spawn._enoent.</span>verifyENOENTSync (status, parsed)](#apidoc.element.cross-spawn._enoent.verifyENOENTSync)
- description and source-code
```javascript
function verifyENOENTSync(status, parsed) {
    if (isWin && status === 1 && !parsed.file) {
        return notFoundError(parsed.original, 'spawnSync');
    }

    // If we are in node 10, then we are using spawn-sync; if it exited
    // with -1 it probably means that the command does not exist
    if (isNode10 && status === -1) {
        parsed.file = isWin ? parsed.file : resolveCommand(parsed.original);

        if (!parsed.file) {
            return notFoundError(parsed.original, 'spawnSync');
        }
    }

    return null;
}
```
- example usage
```shell
...
    // Parse the arguments
    parsed = parse(command, args, options);

    // Spawn the child process
    result = cpSpawnSync(parsed.command, parsed.args, parsed.options);

    // Analyze if the command does not exists, see: https://github.com/IndigoUnited/node-cross-spawn/issues/16
    result.error = result.error || enoent.verifyENOENTSync(result.status, parsed);

    return result;
}

module.exports = spawn;
module.exports.spawn = spawn;
module.exports.sync = spawnSync;
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
