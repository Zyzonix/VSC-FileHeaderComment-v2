# FileHeaderComment v2

Therefore that the author of the original [project](https://github.com/doi/fileheadercomment) did a perfect job but doesn't continue the development of this extension, this fork was created. It's main goal is a further development to add additional features to the extension.

This extension allow you to insert timestamp, copyright or any information to your file like comment below. The extension is able to detect multiple languages to select the correct comment prefix.

	/*
	 * Created on Tue Feb 18 2020
	 *
	 * Copyright (c) 2020 - Your Company
	 */

## Features

- insert defined parameter like `date`, `time`, `datetime`, `filename` (full list can be found [here](#variables))
- insert your own parameter and template
- detect files language to use correct comment prefix (list can be found [here](#language-list))
- define multiple templates

## Quick Jump
- [Updates](#updates)
- [Installation](#installation)
- [Setup](#setup)
- [Usage](#usage)
- [Variables](#variables)
- [Extension settings](#extension-settings)
- [Language list](#language-list)

## Updates
- [1.0.2] Updated install instructions

- [1.0.1] Fixed template variable issue

- [1.0.0] Added support for Makefile

## Installation
There are three ways to install this extension:
- VisualStudio Marketplace (or Extensiontab within VSC)
- manual install of vsix-file from releases
- git-clone and manual package export with vsce

	git clone https://github.com/Zyzonix/VSC-FileHeaderComment-v2.git
	npm install -g vsce
	vsce package


## Setup
Firstly paste the default configuration to your `settings.js`: 

This file can be found under extension settings, keep in mind to edit the correct `settings.js` file in case you are using a SSH-connection or working in a WSL-window.

```
	"fileHeaderComment.parameter":{
		"*":{
			"commentbegin": "/*",
			"commentprefix": " *",
			"commentend": " */",
			"company": "Your Company"
		}
	},
	"fileHeaderComment.template":{
		"*":[
			"${commentbegin}",
			"${commentprefix} Created on ${date}",
			"${commentprefix}",
			"${commentprefix} Copyright (c) ${year} ${company}",
			"${commentend}"
		]
	}
```
## Usage
By default you don't have to set anything. It will detect most programming language for appropriate comment syntax.

Execute it from `Command Pallete` (menu View - Command Pallete... or ctrl+shift+p) then type command below:

1. `FileHeaderComment: Insert Default Template at Cursor`
2. `FileHeaderComment: Select from Available Templates`

The second command will show your available templates defined in Settings

If you want to set your own parameter and template (set from menu Preferences - User Settings), you can read explanation below

## Variables
You can use parameters below in your template

Parameter | Function | Example
---|---|---
`date` | current date | Thu May 26 2022
`dateeurop` | current date (formatted for europe) | 26.05.2022
`time` | current time | 10:23:52 PM
`time24h` | current time in 24 hour format | 22:23:52
`datetime`| current date + time | Thu May 26 2022 11:48:52 PM
`datetime24h` | current date + time in 24 hour format | Thu May 26 2022 23:48:52
`company` | "Your Company" | Company
`day` | day of the month | 26
`month` | current month | 05
`year` | current year | 2022
`hour` | current hour (24h) | 14
`minute` | current minute | 45
`second` | current second | 20
`filename` | filename | file.py
`filewithpath` | filename with filepath | path/to/file.py
`filewithpathandproject` | filename with filepath and project | project/path/to/file.py
`project` | projectname | project

## Language list
The following languages are automatically detected
- Swift
- Lua
- Perl
- Ruby
- Shellscript/Bash
- Yaml
- Makefile
- Python
- VB
- Clojure
- XML
- HTML
- JavaScript
- Java

If there's a language not on the list that you wish to use: set custom prefixes under parameters, see [here](#extension-settings) or request an update via opening an issue.


## Extension settings

Define all custom variables/paramenters in asterisk `*` like

```
"fileHeaderComment.parameter":{
	"*":{
		"company": "Your Company"
		"myvar1": "My Variable 1",
		"myvar2": "My Variable 2"
	}
}
```

Use your variable in template like (asterisk `*` will be default template)

```
"fileHeaderComment.template":{
	"*":[
		"${commentbegin}",
		"${commentprefix} Created on ${date}",
		"${commentprefix}",
		"${commentprefix} Copyright (c) ${year} ${company}",
		"${commentprefix} my variables are ${myvar1} and ${myvar2}",
		"${commentend}"
	]
}
```
You can define multiple templates, for instance template for MIT License

```
"fileHeaderComment.parameter":{
	"*":{
		"author": "Your Name"
	},
	"mit":{
		"license_mit":[
			"The MIT License (MIT)",
			" Copyright (c) ${year} ${author}",
			"",
			" Permission is hereby granted, free of charge, to any person obtaining a copy of this software",
			" and associated documentation files (the \"Software\"), to deal in the Software without restriction,",
			" including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense,",
			" and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so,",
			" subject to the following conditions:",
			"",
			" The above copyright notice and this permission notice shall be included in all copies or substantial",
			" portions of the Software.",
			"",
			" THE SOFTWARE IS PROVIDED \"AS IS\", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED",
			" TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL",
			" THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,",
			" TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE."
		]
	}

},
"fileHeaderComment.template":{
	"*":[
		"${commentbegin}",
		"${commentprefix} Created by ${author}",
		"${commentend}"
	],
	"mit":[
		"${commentbegin}",
		"${commentprefix} Created on ${date}",
		"${commentprefix}",
		"${commentprefix} ${license_mit}",
		"${commentend}"
	]
}
```
You can use your `mit` template above by calling it through `Command Pallete` and choose `FileHeaderComment: Select from Available Templates`.

You can set also custom comment prefixes if your language is not automatically detected:

```
"fileHeaderComment.parameter":{
	"your_language":{
		"commentbegin": "#",
		"commentprefix": "#",
		"commentend": "#",
		"author": "Your name"
	}
},
"fileHeaderComment.template":{
	"your_language":{
		"${commentbegin}",
		"${commentprefix} Created by ${author}",
		"${commentend}"
	}
}
```

Readme version: 1.6
