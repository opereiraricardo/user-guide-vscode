# Integrate with External Tools via Tasks

Lots of tools exist to automate tasks like linting, building, packaging, testing, or deploying software systems. Examples include the [TypeScript Compiler](https://www.typescriptlang.org/), linters like [ESLint](https://eslint.org/) and [TSLint](https://palantir.github.io/tslint/) as well as build systems like [Make](https://en.wikipedia.org/wiki/Make_(software)), [Ant](https://ant.apache.org/), [Gulp](https://gulpjs.com/), [Jake](https://jakejs.com/), [Rake](https://ruby.github.io/rake/), and [MSBuild](https://github.com/dotnet/msbuild).

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/tasks_hero.png)

These tools are mostly run from the command line and automate jobs inside and outside the inner software development loop (edit, compile, test, and debug). Given their importance in the development life cycle, it is helpful to be able to run tools and analyze their results from within VS Code. Tasks in VS Code can be configured to run scripts and start processes so that many of these existing tools can be used from within VS Code without having to enter a command line or write new code. Workspace or folder specific tasks are configured from the `tasks.json` file in the `.vscode` folder for a workspace.

Extensions can also contribute tasks using a [Task Provider](https://code.visualstudio.com/api/extension-guides/task-provider), and these contributed tasks can add workspace-specific configurations defined in the `tasks.json` file.


> **Note:**
> Task support is only available when working on a workspace folder. It is not available when editing single files

# [TypeScript Hello World](https://code.visualstudio.com/docs/editor/tasks#_typescript-hello-world)

Let's start with a simple "Hello World" TypeScript program that we want to compile to JavaScript.

Create an empty folder "mytask", generate a `tsconfig.json` file and start VS Code from that folder.

```
mkdir mytask
cd mytask
tsc --init
code .
```

Now create a `HelloWorld.ts` file with the following content

```
function sayHello(name: string): void {
  console.log(`Hello ${name}!`);
}

sayHello('Dave');
```

Pressing `Ctrl+Shift+B` or running **Run Build Task** from the global **Terminal** menu show the following picker:

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/typescript-build.png)


The first entry executes the TypeScript compiler and translates the TypeScript file to a JavaScript file. When the compiler has finished, there should be a `HelloWorld.js` file. The second entry starts the TypeScript compiler in watch mode. Every save to the `HelloWorld.ts` file will regenerate the `HelloWorld.js` file.

You can also define the TypeScript build or watch task as the default build task so that it is executed directly when triggering **Run Build Task** `Ctrl+Shift+B`. To do so, select `Configure Default Build Task` from the global `Terminal` menu. This shows you a picker with the available build tasks. Select `tsc: build` or `tsc: watch` and VS Code will generate a `(tasks.json` file. The one shown below makes the `tsc: build` task the default build task:

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "typescript",
      "tsconfig": "tsconfig.json",
      "problemMatcher": ["$tsc"],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

The `tasks.json` example above does not define a new task. It annotates the tsc: build tasks contributed by VS Code's TypeScript extension to be the default build task. You can now execute the TypeScript compiler by pressing `Ctrl+Shift+B`

# [Task auto-detection](https://code.visualstudio.com/docs/editor/tasks#_task-autodetection)


VS Code currently auto-detects tasks for the following systems: Gulp, Grunt, Jake, and npm. We are working with the corresponding extension authors to add support for Maven and the C# `dotnet` command as well. If you develop a JavaScript application using Node.js as the runtime, you usually have a `package.json` file describing your dependencies and the scripts to run. If you have cloned the [eslint-starter](https://github.com/megamaddu/eslint-starter) example, then executing **Run Tasks** from the global menu shows the following list:

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/eslint-starter.png)

If you have not already done so, install the necessary npm modules by running `npm install`. Now open the `(server.js)` file and add a semicolon to the end of a statement (note the ESLint starter assumes statements without a semicolon) and execute the **Run Tasks** again. This time select the **npm: lint** task. When prompted for the problem matcher to use, select **ESLint stylish**

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/eslint-problem-matcher-selection.png)

### Executing the task produces one error, shown in the **Problems** view:

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/eslint-problem.png)

In addition, VS Code created a `tasks.json` file with the following content:

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "npm",
      "script": "lint",
      "problemMatcher": ["$eslint-stylish"]
    }
  ]
}
```

This instructs VS Code to scan the output of the `npm lint` script for problems using the ESLint stylish format.

For Gulp, Grunt, and Jake, the task auto-detection works the same. Below is an example of the tasks detected for the [vscode-node-debug](https://github.com/microsoft/vscode-node-debug) extension.

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/gulp-auto-detect.png)

> Tip: You can run your task through **Quick Open** `(Ctrl+P)` by typing 'task', `Space` and the command name. In this case, 'task lint'.

Task auto detection can be disabled using the following settings:

```
{
  "typescript.tsc.autoDetect": "off",
  "grunt.autoDetect": "off",
  "jake.autoDetect": "off",
  "gulp.autoDetect": "off",
  "npm.autoDetect": "off"
}
```

# [Custom tasks](https://code.visualstudio.com/docs/editor/tasks#_custom-tasks)

Not all tasks or scripts can be auto-detected in your workspace. Sometimes it is necessary to define your own custom tasks. Assume you have a script to run your tests in order to set up some environment correctly. The script is stored in a script folder inside your workspace and named `test.sh` for Linux and macOS and `test.cmd` for Windows. Run **Configure Tasks** from the global **Terminal** menu and select the **Create tasks.json file from template** entry. This opens the following picker:

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/configure-task-runner.png)


> **Note:**
> If you don't see the list of task runner templates, you may already have a `tasks.json` file in your folder and its contents will be open in the editor. Close the file and either delete or rename it for this example.

We are working on more auto-detection support, so this list will get smaller and smaller in the future. Since we want to write our own custom task, select **Others** from the list. This opens the `tasks.json` file with a task skeleton. Replace the contents with the following:

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run tests",
      "type": "shell",
      "command": "./scripts/test.sh",
      "windows": {
        "command": ".\\scripts\\test.cmd"
      },
      "group": "test",
      "presentation": {
        "reveal": "always",
        "panel": "new"
      }
    }
  ]
}
```

The task's properties have the following semantic:

- **label**: The task's label used in the user interface.
- type: The task's type. For a custom task, this can either be `shell` or `process`. If `shell` is specified, the command is interpreted as a shell command (for example: bash, cmd, or PowerShell). If `process` is specified, the command is interpreted as a process to execute.
- **command**: The actual command to execute.
- **windows**: Any Windows specific properties. Will be used instead of the default properties when the command is executed on the Windows operating system.
- **group**: Defines to which group the task belongs. In the example, it belongs to the test group. Tasks that belong to the `test` group can be executed by running **Run Test Task** from the **Command Palette**.
- **presentation**: Defines how the task output is handled in the user interface. In this example, the Integrated Terminal showing the output is `always` revealed and a `new terminal` is created on every task run.
- **options**: Override the defaults for `cwd` (current working directory), `env` (environment variables), or `shell` (default shell). Options can be set per task but also globally or per platform. Environment variables configured here can only be referenced from within your task script or process and will not be resolved if they are part of your args, command, or other task attributes.
- **runOptions**: Defines when and how a task is run.

You can see the full set of task properties and values with IntelliSense in your `tasks.json` file. Bring up suggestions with **Trigger Suggest** (`Ctrl+Space`) and read the descriptions on hover or with the **Read More**... ('i') flyout.

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/tasks-intellisense.png)

You can also review the [tasks.json schema](https://code.visualstudio.com/docs/editor/tasks-appendix).

Shell commands need special treatment when it comes to commands and arguments that contain spaces or other special characters like `$`. By default, the task system supports the following behavior:

- If a single command is provided, the task system passes the command as is to the underlying shell. If the command needs quoting or escaping to function properly, the command needs to contain the proper quotes or escape characters. For example, to list the directory of a folder containing spaces in its name, the command executed in bash should look like this: `ls 'folder with spaces'`.

```
{
  "label": "dir",
  "type": "shell",
  "command": "dir 'folder with spaces'"
}
```

- If a command and arguments are provided, the task system will use single quotes if the command or arguments contain spaces. For `cmd.exe`, double quotes are used. A shell command like below will be executed in PowerShell as `dir 'folder with spaces'`.

```
{
  "label": "dir",
  "type": "shell",
  "command": "dir",
  "args": ["folder with spaces"]
}
```

- If you want to control how the argument is quoted, the argument can be a literal specifying the value and a quoting style. The example below uses escaping instead of quoting for an argument with spaces.

```
{
  "label": "dir",
  "type": "shell",
  "command": "dir",
  "args": [
    {
      "value": "folder with spaces",
      "quoting": "escape"
    }
  ]
}
```

Besides escaping, the following values are supported:

- **strong**: Uses the shell's strong quoting mechanism, which suppresses all evaluations inside the string. Under PowerShell and for shells under Linux and macOS, single quotes are used (`'`). For cmd.exe, `"` is used.
- **weak**: Uses the shell's weak quoting mechanism, which still evaluates expression inside the string (for example, environment variables). Under PowerShell and for shells under Linux and macOS, double quotes are used (`"`). cmd.exe doesn't support weak quoting so VS Code uses `"` as well.
If the command itself contains spaces, VS Code will by default strong quote the command as well. As with arguments, the user can control the quoting of the command using the same literal style.

There are more task properties to configure your workflow. You can use IntelliSense with `Ctrl+Space` to get an overview of the valid properties.

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/intellisense.png)

In addition to the global menu bar, task commands can be accessed using the **Command Palette** (`Ctrl+Shift+P`). You can filter on 'task' and can see the various task related commands.

![Imagem](https://code.visualstudio.com/assets/docs/editor/tasks/command-palette.png)

[Compound tasks](https://code.visualstudio.com/docs/editor/tasks#_compound-tasks)

You can also compose tasks out of simpler tasks with the `dependsOn` property. For example, if you have a workspace with a client and server folder and both contain a build script, you can create a task that starts both build scripts in separate terminals. If you list more than one task in the `dependsOn` property, they are executed in parallel by default.

The `tasks.json` file looks like this:

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Client Build",
      "command": "gulp",
      "args": ["build"],
      "options": {
        "cwd": "${workspaceFolder}/client"
      }
    },
    {
      "label": "Server Build",
      "command": "gulp",
      "args": ["build"],
      "options": {
        "cwd": "${workspaceFolder}/server"
      }
    },
    {
      "label": "Build",
      "dependsOn": ["Client Build", "Server Build"]
    }
  ]
}
```

If you specify `"dependsOrder": "sequence"`, then your task dependencies are executed in the order they are listed in `dependsOn`. Any background/watch tasks used in `dependsOn` with `"dependsOrder": "sequence"` must have a problem matcher that tracks when they are "done". The following task runs task Two, task Three, and then task One.

```
{
  "label": "One",
  "type": "shell",
  "command": "echo Hello ",
  "dependsOrder": "sequence",
  "dependsOn": ["Two", "Three"]
}
```

[User level tasks](https://code.visualstudio.com/docs/editor/tasks#_user-level-tasks)

You can create user level tasks that are not tied to a specific workspace or folder using the **Tasks: Open User Tasks** command. Only `shell` and `process` tasks can be used here since other task types require workspace information.

[Output behavior](https://code.visualstudio.com/docs/editor/tasks#_output-behavior)

Sometimes you want to control how the Integrated Terminal panel behaves when running tasks. For instance, you may want to maximize editor space and only look at task output if you think there is a problem. The behavior of the terminal can be controlled using the `presentation` property of a task. It offers the following properties:

- **reveal**: Controls whether the Integrated Terminal panel is brought to front. Valid values are:
    - `always` - The panel is always brought to front. This is the default.
    - `never` - The user must explicitly bring the terminal panel to the front using the **View > Terminal** command (`Ctrl+` `).
    - `silent` - The terminal panel is brought to front only if the output is not scanned for errors and warnings.
- **revealProblems**: Controls whether the Problems panel is revealed when running this task or not. Takes precedence over option `reveal`. Default is `never`.
    - `always` - Always reveals the Problems panel when this task is executed.
    - `onProblem` - Only reveals the Problems panel if a problem is found.
    - `never` - Never reveals the Problems panel when this task is executed.
- **focus**: Controls whether the terminal is taking input focus or not. Default is `false`.
- **echo**: Controls whether the executed command is echoed in the terminal. Default is `true`.
- **showReuseMessage**: Controls whether to show the "Terminal will be reused by tasks, press any key to close it" message.
- **panel**: Controls whether the terminal instance is shared between task runs. Possible values are:
    - `shared` - The terminal is shared and the output of other task runs are added to the same terminal.
    - `dedicated` - The terminal is dedicated to a specific task. If that task is executed again, the terminal is reused. However, the output of a different task is presented in a different terminal.
    - `new` - Every execution of that task is using a new clean terminal.
- **clear**: Controls whether the terminal is cleared before this task is run. Default is `false`.
- **close**: Controls whether the terminal the task runs in is closed when the task exits. Default is `false`.
- **group**: Controls whether the task is executed in a specific terminal group using split panes. Tasks in the same group (specified by a string value) will use split terminals to present instead of a new terminal panel.

You can modify the terminal panel behavior for auto-detected tasks as well. For example, if you want to change the output behavior for the **npm: run lint** from the ESLint example from above, add the `presentation` property to it:

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "npm",
      "script": "lint",
      "problemMatcher": ["$eslint-stylish"],
      "presentation": {
        "reveal": "never"
      }
    }
  ]
}
```

You can also mix custom tasks with configurations for detected tasks. A `tasks.json` that configures the **npm: run lint** task and adds a custom **Run Test** tasks looks like this:

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "npm",
      "script": "lint",
      "problemMatcher": ["$eslint-stylish"],
      "presentation": {
        "reveal": "never"
      }
    },
    {
      "label": "Run tests",
      "type": "shell",
      "command": "./scripts/test.sh",
      "windows": {
        "command": ".\\scripts\\test.cmd"
      },
      "group": "test",
      "presentation": {
        "reveal": "always",
        "panel": "new"
      }
    }
  ]
}
```
[Run behavior](https://code.visualstudio.com/docs/editor/tasks#_run-behavior)

You can specify a task's run behaviors using the `runOptions` property:

- **reevaluateOnRerun**: Controls how variables are evaluated when a task is executed through the **Rerun Last Task** command. The default is `true`, meaning that variables will be reevaluated when a task is rerun. When set to `false` the resolved variable values from the previous run of the task will be used.
- **runOn**: Specifies when a task is run.
    - `default` - The task will only be run when executed through the Run Task command.
    - `folderOpen` - The task will be run when the containing folder is opened. The first time you open a folder that contains a task with `folderOpen`, you will be asked if you want to allow tasks to run automatically in that folder. You can change your decision later using the **Manage Automatic Tasks** command and selecting between **Allow Automatic Tasks** and **Disallow Automatic Tasks**.


[Customizing auto-detected tasks](https://code.visualstudio.com/docs/editor/tasks#_customizing-autodetected-tasks)

As mentioned above, you can customize auto-detected tasks in the `tasks.json` file. You usually do so to modify presentation properties or to attach a problem matcher to scan the task's output for errors and warnings. You can customize a task directly from the **Run Task** list by pressing the gear icon to the right to insert the corresponding task reference into the `tasks.json` file. Assume you have the following Gulp file to lint JavaScript files using ESLint (the file is taken from [https://github.com/adametry/gulp-eslint](https://github.com/adametry/gulp-eslint)):

```
const gulp = require('gulp');
const eslint = require('gulp-eslint');

gulp.task('lint', () => {
  // ESLint ignores files with "node_modules" paths.
  // So, it's best to have gulp ignore the directory as well.
  // Also, Be sure to return the stream from the task;
  // Otherwise, the task may end before the stream has finished.
  return (
    gulp
      .src(['**/*.js', '!node_modules/**'])
      // eslint() attaches the lint output to the "eslint" property
      // of the file object so it can be used by other modules.
      .pipe(eslint())
      // eslint.format() outputs the lint results to the console.
      // Alternatively use eslint.formatEach() (see Docs).
      .pipe(eslint.format())
      // To have the process exit with an error code (1) on
      // lint error, return the stream and pipe to failAfterError last.
      .pipe(eslint.failAfterError())
  );
});

gulp.task('default', ['lint'], function() {
  // This will only run if the lint task is successful...
});
```

Executing **Run Task** from the global **Terminal** menu will show the following picker:

![Image](https://code.visualstudio.com/assets/docs/editor/tasks/configure-tasks.png)

Press the gear icon. This will create the following `tasks.json` file:

```
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "type": "gulp",
      "task": "default",
      "problemMatcher": []
    }
  ]
}
```

Usually you would now add a problem matcher (in this case `$eslint-stylish`) or modify the presentation settings.

