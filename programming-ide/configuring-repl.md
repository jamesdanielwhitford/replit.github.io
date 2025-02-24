# Configuring a Repl

A file named `.replit` can be added to or edited in any repl in order to customize the behavior of the repl. Used in combination with [nix](/programming-ide/getting-started-nix) for installed linux packages, the sky is the limit! 

Many repls are preconfigured with a `.replit` file which can be found by clicking the three dot menu in the file tree and selecting `Show hidden files`.

Written in [toml](https://github.com/toml-lang/toml), a `.replit` file looks something like:

```toml
# The command that is executed when the run button is clicked.
run = ["cargo", "run"]

# The default file opened in the editor.
entrypoint = "src/main.rs"

# Setting environment variables
[env]
FOO="foo"

# Packager configuration for the Universal Package Manager
# See https://github.com/replit/upm for supported languages.
[packager]
language = "rust"

  [packager.features]
  # Enables the package search sidebar
  packageSearch = true
  # Enabled package guessing
  guessImports = false

# Per language configuration: language.<lang name> 
[languages.rust]
# The glob pattern to match files for this programming language
pattern = "**/*.rs"

    # LSP configuration for code intelligence
    [languages.rust.languageServer]
    start = ["rust-analyzer"]
```

Here's a short video on how to use the `.replit` file or read the text explanation below.
 
<iframe width="560" height="315" src="https://www.youtube.com/embed/vDlCkQ9-ErU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In the snippet above, `run` is a string which will be executed in the shell whenever you hit the "Run" button. The `language` helps the IDE understand how to provide features like [packaging](https://blog.replit.com/upm) and [code intelligence](https://blog.replit.com/intel). This is normally configured for you when you clone from a Git repository.

Here is an example of a repl using `.replit` to print "hello world" instead of running the code:

<iframe width="100%" src="https://replit.com/@turbio/dotreplit-example?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

## Configuring a Cloned Repl

When you clone a repository without a `.replit` file, we automatically show the visual `.replit` editor:

![visual config editor](https://docs.replit.com/images/config_plugin.png)

This will automatically create the `.replit` file and make it possible to customize how the repl will run. You can use the shell to run any command and then set the "Run" button once you've decided what it should do. Clicking "done" will finalize the repl's configuration and close the visual editor. It's always possible to make changes later by visiting the `.replit` file from the filetree. Adding `.replit` to a repository makes cloning fast with no configuration necessary. 

# Other Configuration
The `.replit` file can also provide other configuration hints. The full specification is provided below:

- `run`: Command - Command that is executed when the run button is clicked
- `language`: Reserved
- `audio`: Boolean - Whether [system-wide audio](https://docs.replit.com/misc/playing-audio-replit) is enabled for this repl.
- `[env]`: Setting environment variables
- `[packager]`: Package management configuration.
    - `afterInstall`: Command - Command that is executed after a new package is installed
    - `ignoredPaths`: List of Strings - List of paths to ignore while attempting to guess packages ([More about installing packages](https://docs.replit.com/repls/packages/#DirectImports))
    - `ignoredPackages`: List of strings - List of modules to never attempt to guess a package for, when installing packages ([More about installing packages](https://docs.replit.com/repls/packages/#DirectImports))
    - `language`: String - Specified the language to use for package operations. See available languages in the [Universal Package Manager](https://github.com/replit/upm) repository.
    - `features`: UPM features that are supported by the specified languages.
        - `packageSearch`: Boolean - If enabled, a package search panel will be available in the sidebar.
        - `guessImports`: Boolean - If enabled, UPM will attempt to guess which packages need to be installed prior to running the repl.
- `languages.<language name>`: Per-language configuration. The language name has no special meaning other than to allow multiple languages to be configured at once.
    - `pattern`: String - A [glob](https://en.wikipedia.org/wiki/Glob_(programming)) used to identify which files belong to this language configuration. (Example: `**/*.js`)
    - `languageServer`: Configuration for setting up [LSP](https://microsoft.github.io/language-server-protocol/) for this language. This allows for code intelligence (autocomplete, underlined errors, etc...)
        - `start`: Command - The command used to start the LSP server
        
### Command
A command can either be a string or a list of strings. If the command is a string (`"node index.js"`), it will be executed via `sh -c "<command>"`. If the command is a list of strings (`["node", "index.js"]`), it will be directly executed with the list of strings passed as arguments. When possible, it is preferred to pass a list of strings.

## Example .replit File

```toml
run="python main.py"
language="python3"
onBoot="echo Booting up!"

[packager]
afterInstall="date >> package_install_log"
ignoredPaths=[".git"]
ignoredPackages=["twitter", "discord"]
```

## HTML

For HTML projects, you can keep the run command empty and we will serve the project for you automatically. As per web standards, the entrypoint file is `index.html`. If you want to serve a different file, you can roll your own webserver in one of the languages that we support. 

We created an [example](https://replit.com/@amasad/run-html-non-index-file) for you in NodeJS that serves `foo.html` instead of `index.html`. Otherwise it works like any other HTML project.
