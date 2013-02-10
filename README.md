# ac-js2


An attempt at context sensitive auto-completion for Javascript in Emacs using
Js2-mode's parser and Skewer-mode. Inspired by the work of others on
projects such as Js2-mode, Skewer-mode and Js2-refactor I decided to
add to the concept of Emacs as a Javascript IDE.

Here is a screenshot of the auto completion in action.

![Completion](https://raw.github.com/ScottyB/ac-js2/master/images/function-interface.png)

## Features

 * Auto complete with js2-browser-externs
 * Auto complete with js2-keywords
 * Auto complete with js2-ecma-262-externs

Each of the above settings can be customized and are enabled by default.

 * Partial support for completing properties
 * Show function interface or initial value for object properties
 * Support for external libraries

Ac-js2 uses Skewer-mode to evaluate Javascript code in the browser
which could have undesired side effects. Therefore these features are
turned off by default, see Setup to enable these features anyway :).

 * Navigation commands to jump to variables, functions and object properties.

Jumping to values in an object literal isn't currently supported, it
is on my todo list though. Navigation works from anywhere along a dotted property reference.
i.e. Given the following proprety reference:

```
foo.bar.baz();
```

placing the cursor on `foo`, `bar` or `baz` and executing
`ac-js2-jump-to-definition` or `M-.` will take you straight to their respective
definitions.

 * Completion of variable and function names in current scope
 * Popup documentation for variables and function names in buffer

**Note:** Navigation only works if the definition is in the same file.

## Installation

Intergration with a package manager will be coming soon. For now clone
this repository and fetch the dependencies using the built in package
manager. You may need to add the following to your init.el to be able
to fetch skewer-mode from melpa.

```
(add-to-list 'package-archives
              '("melpa" . "http://melpa.milkbox.net/packages/") t)
```

### Dependencies

 * [skewer-mode](https://github.com/skeeto/skewer-mode) (MELPA)
 * [js2-mode](https://github.com/mooz/js2-mode) (ELPA)
 * [auto-complete](https://github.com/auto-complete/auto-complete) (ELPA)

Make sure auto-complete-mode is enabled for all buffers with the following command.

```
(global-auto-complete-mode)
```

## Setup

Add the following to your init.el:

```
(add-to-list 'load-path "/path/to/ac-js2")
(require 'ac-js2)
```

Copy the snippet below if you want to evaluate your Javascript code
for candidates. Not setting this value will still provide you with basic completion.
Something that I hope to improve in the future.

```
(setq ac-js2-evaluate-calls t)
```

Add any external Javascript files to the variable below. Make sure you
have initialised `ac-js2-evaluate-calls` to t if you add any libraries.

```
(add-to-list 'ac-js2-external-libraries "full/path/to/a-library.js")
```

## Usage

Call `run-skewer` and open up a Javascript file. If
`ac-js2-evaluate-calls` is t then make a minor change and save the file
to get completions for objects in buffer.
