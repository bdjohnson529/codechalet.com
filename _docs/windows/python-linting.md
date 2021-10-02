---
title: "Python Linting in Sublime"
layout: blog
topic: Windows
topic_path: /docs/windows/index.html
---
Linters are tools which analyze source code to flag functional and stylistic errors. You've probably seen linting in action - if you've ever used SQL Server Management Studio, the application will highlight parts of your query which are incorrect. Linters are helpful tools to increase the quality of source code. They are especially helpful to enforce stylistic conventions on a software development team.

## Sublime Linter
[SublimeLinter](https://github.com/SublimeLinter/SublimeLinter#SublimeLinter) is Sublime's linting package. The package is a linting *framework* - it does not ship with any actual linters. Linters must be installed separately.

Install SublimeLinter using Package Control.
* Launch Package Control : `(Ctrl+Shift+P)`
* Install a new package : `Package Control: Install Package`
* Select SublimeLinter : `SublimeLinter`


## Flake8
[Flake8](https://flake8.pycqa.org/en/latest/) is a Python linter.

Install Flake8, using `pip`. It is recommended to install Flake8 in a virtual environment to avoid permissions issues.
```bash
conda create -n lintenv python=3.6
conda activate lintenv
conda install -c anaconda flake8
```

Find the executable path. We will use this when configuring Sublime.
```bash
where flake8
```


**Install SublimeLinter-Flake8.**
* Launch Package Control : `(Ctrl+Shift+P)`
* Install a new package : `Package Control: Install Package`
* Select SublimeLinter : `SublimeLinter-flake8`

**Configure Sublime settings to use Flake8.**
* Select `Preferences -> Package Settings -> SublimeLinter -> Settings`
* Add the following lines to the User settings. Replace the executable path with the path to your executable.
```json
    "linters": {
        "flake8": {
            "@disable": false,
            "args": [],
            "builtins": "",
            "excludes": [],
            "ignore": "",
            "max-complexity": 10,
            "max-line-length": null,
            "select": "",
            "executable": ["C:\\Users\\username\\anaconda3\\envs\\lintenv\\Scripts\\flake8.exe"],
        }
    },
```

## Usage
Use the [SublimeLinter key bindings](https://github.com/SublimeLinter/SublimeLinter#Key-Bindings) to run Flake8 in Sublime.