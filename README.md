# tasks.json for fpm (fortran package manager) projects

This tasks.json file associates `fpm build` and `fpm test` commands with a build and a test task in VS Code, respectively.
tasks.json also provides `fpm run` and `fpm install` task. `fpm install` task installs the executable target to `./build` directory.
`run` task calls `fpm install` before executes the command, demonstrating the usage of `dependsOn`.

## Requirement

- VSCode
- fpm (fortran package manager) ver. 0.1 or later.

## Usage

- Pressing `Ctrl+Shift+B` executes `fpm build` command.
- Running `Run Test Task` from the VSCode's command palette executes `fpm test` command.
  - Binding a keyboard shortcut to `workbench.action.tasks.test` may make it easier to run the test task.

## Install

1. create a new fpm project by `fpm new` command.
1. create `.vscode` directory in the project root directory
1. copy the tasks.json to the `.vscode` directory

## Licence

[MIT](https://github.com/tcnksm/tool/blob/master/LICENCE)

## Author

[Tomohiro Degawa](https://github.com/degawa)