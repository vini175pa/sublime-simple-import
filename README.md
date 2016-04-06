Simple Import JS
===================

`Simple import` is a plugin for Sublime Text that imports your modules. Just select select the module you want to import and select "Simple Import: insert imports". You can import as many modules you want at once.

![Example image](https://raw.githubusercontent.com/vini175pa/sublime-simple-import/master/example.gif)


Installing
----------

### With Package Control (recommended)
1. Install [Package Control](https://sublime.wbond.net/installation)
2. Run “Package Control: Install Package” command
3. Find and install the `Simple Import` plugin.
4. Restart Sublime Text if there are issues.

### Manually

Clone the repository in your Sublime Text "Packages" directory:

    git clone https://github.com/vini175pa/sublime-simple-import.git

The "Packages" directory is located at:

* OS X: `~/Library/Application Support/Sublime Text 3/Packages/`

* Linux: `~/.config/sublime-text-3/Packages/`

* Windows: `%APPDATA%\Sublime Text 3\Packages\`


Syntax
-------------

`[![@]]Name[:Module][:$]`

This is the syntax. Simple Import offers you some to import a module, like, where should it be searched, the searching um be case insensitive or not, and more. But wait, isn't this plugin SIMPLE? Yes, it its. Let's have a look.

**Name** is the variable name that will be used

**Module** ... common? Have a guess!

'**:**' separates the parts.

**@** Indicates if this should be searched or not. This is **True** by default

**!** Indicates if the search will be case sensitive or not. **True** by default

**$** Indicates if this is a ES6 Syntax import or not. If you add this, you will have `const Name = require("Module")`

 **Important - **  Double Separators between the Name and the Module make it an "import from property from module "

	A::B`    = `import { A } from 'B'
	A::B:$`  = `const A = require('B').A
	*::A`    = `import * as A from 'A'
	*::A:B`  = `import * as A from 'B'

Every indicator or default setting can be defined in your project and in your sublime settings. Look at  [Configurations](#configurations) (optional)

Let's say you want to import `React`. Just add `React`, use the simple-import and BAM! `import React from react;` will be added at the top of your file. But what if you wanted set another variable instead of React? Use `NameYouWant:react` and it's gonna work: `import NameYouWant 'react'`

Lets say you have something like this:

	src/
		components/
			Login/
				index.jsx
			Register/
				index.jsx
			Home/
				index.js
		elements/
			input.jsx

If you try to import `index`, a dropdown will be open and show you the options. But, if you want to import an specific file, simply import `Login/index` and it's going to work.

Searching accepts some flags. Examples: `components/*/index`, `components/*/i*`, have fun!

----------

Configurations
-------------

To configurate Simple Import you can do 2 this. You can create a file on the root of your project called `.simple-import.json`. **IMPORTANT** This is a json file.

Example:

	{
		"excluded_directories" : [ ... ],
		...
	}


You can set `"simple-import" : { <here comes the settings> }` at your sublime settings to. ( **Preferences > Settings - User** )


## Options

**excluded_directories**  (Array) :   Directories that wont be matched. Example: `["node_modules", ".git"]`

**extensions**  (Array) :   Extensions to be matched on search and will be removed from file on import . Don't add "." (dot). **Default** `[ "js" ]`

**separator** (String) : The separator between imports. **Default** `;`

**name_separator** (String) : The separator. **Default** `:`

**from_indicator** (String) : Indicator that this is a "import of property". **Default** `::`

**remove_index_from_path** (Boolean): Indicates whether it should remove an `index` file from a path or not. Example `../Login/index` is modified to `../Login`. **Default** True

**search_indicator** (String): Indicator that it should search for a file or not. **Default** `@`

**search_ignorecase_indicator** (String) : Indicator that the search will be case sensitive or not.  **Default** `!`

**settings_file** (String) :  The path of the settings file for Simple Import. **Default** `.simple-import`

**search_by_default** (Boolean): Indicates if by default an import should do a search. The Search Indicator (`@`) makes the import do the opposite of the default. **Default** `True`

**search_ignorecase_by_default** :  (Boolean): Indicates if by default an import should do a search case insensitive ( ignore the cases) . The Ignore Case Indicator (`!`) makes the import do the opposite of the default. **Default** `True`

**es6_by_default** :  (Boolean): Indicates if by default an import should be an `import` or a `require`.  A `$` at the end of an import makes it do the opposite of the default. **Default** `True`


## Different settings for each path

If you want to use different settings for specific folders or files you can! In your `.simple-import.json` set only `paths`. Let's see an example:

	{
		"paths": {

			"nodejs" : [ "sockets.js",  "app.js", "routes", "passport", "models", "lib",
				{
					"es6_by_default": false,
					"excluded_directories": [ "react", "node_modules", ".git", "src" ]
				}
			],

			"react/components" : {
				"extensions": ["js", "jsx"]
			}

		}
	}

It only works on your `.simple-import.json` and won't work on sublime settings.



# Key Binding
They are added by default, but if you want to change them just add in your **Preferences > Key Bindings - User**:

	{ "keys": ["ctrl+alt+j"], "command": "simple_import"},
	{ "keys": ["ctrl+alt+i"], "command": "simple_import", "args": { "insert": true}}

Simple Import's Goal
-------------
Simple Import is being built to help importing any module in any language not only JS. Version 2.x will soon be released bringing huge updates. It is being totally rewritten to better handle imports in any language based on a json that will hold the way importing works on each language. Therefore, adding support to a new language will be easy, by just adding:
```
...
"Sass": {
   "extensions": ["scss", "sass"]
   "imports": [
   	{ 
   	   "tests": [ "{module}", "@import {module}"],
   	   "result": "@import '{module}'"
   	}
   ]
}
...
```


Contributing
-------------
Just be nice. Any name you don't agree with, bugs or suggestions, [create an Issue](https://github.com/vini175pa/simple-import-js/issues)! This helps a lot!

... And have in your mind that i'm not a python expert. This is my first module with python, actually.
