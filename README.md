# tasks.json for fpm (fortran package manager) projects

This tasks.json file associates `fpm build` and `fpm test` commands with a build and a test task in VS Code, respectively.
tasks.json also provides `fpm run` and `fpm install` task. `fpm install` task installs the executable target to `./build` directory. Runnging this task before debugging may reduce the complexity of debugging task. (see :[launch.json for debugging an executable target built using fpm](#launchjson))
`run` task calls `fpm install` before executes the command, demonstrating the usage of `dependsOn`.

## Requirement

- VSCode
- fpm (fortran package manager) ver. 0.1 or later.

## Usage
- Put tasks.json to .vscode directory.
- Pressing `Ctrl+Shift+B` executes `fpm build` command.
- Running `Run Test Task` from the VSCode's command palette executes `fpm test` command.
  - Binding a keyboard shortcut to `workbench.action.tasks.test` may make it easier to run the test task.

## Install

1. create a new fpm project by `fpm new` command.
1. create `.vscode` directory in the project root directory
1. copy the tasks.json to the `.vscode` directory

## Additional Option
A code snippet below for specifying shell options may be required for the command prompt in Windows.

```JSON
    "options": {
        "shell": {
            "executable": "${env:windir}\\system32\\cmd.exe",
            "args": [
                "/d",
                "/c"
            ]
        }
    },
```

## launch.json for debugging an executable target built using fpm
<a id="launchjson"></a>
fpm creates a build directory with a different name depending on the profile and compiler flag and builds an executable target in it. This behavior makes debugging troublesome when using VSCode, because we cannot reuse the path to the program to be executed in `launch.json`.

The path setting can be commonized by executing the `fpm install` command to place the executable target in a common path `${workspaceFolder}/build/bin/`.

```JSON
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build/bin/\"put executable name here\"",
            "args": [],
            "stopAtEntry": true,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
```
## Licence

[MIT](https://github.com/tcnksm/tool/blob/master/LICENCE)

## Author

[Tomohiro Degawa](https://github.com/degawa)