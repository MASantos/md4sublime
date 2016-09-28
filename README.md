# md4sublime
Wrapper around pandoc for working with markdown files in sublime.

Creates sublime builds for browser rendering and pdf generation from markdown files.
---
## Requirements
This script requires [`pandoc`](https://en.wikipedia.org/wiki/Pandoc), a document converter written in [Haskell](https://en.wikipedia.org/wiki/Haskell_(programming_language)). Hence, you'll need to install first Haskell, then Pandoc, before making use of this script. 

Note: Read the above link for Pandoc, if you don't know yet what it does. If you work with different document types it may be worth to have Pandoc -even if for that you need Haskell installed.

## STATUS
Only tested for the following environment:
* OSX 10.6.8 Snow Leopard (I know, I know,...walking alone in the desert :-p )
* Firefox
* Sublime Text 2

Actually, I have tested it as well for Firefox and Sublime Text 2 & 3 in Debian 8 Jessie (latest as of Sept. 2016). However only through manual installation and only so for previous versions (as of Wed Sep 28).

## Sublime user defined builds
In order to build a project in sublime one can go to `Tools -> Build System` and choose the one appropiate to our project (say `Make` or `C++` or `Python`) and then triggered it on the file we are currently editing by clicking on `Tools -> Build` ( `command+B/ctrl+B` in Mac/:Linux.

Under `Packages/User` `Sublime Text` lets you define different build methods. These are given in JSON format.
The format is
```JSON
{
  "cmd": ["_build-script_","_args_", "$file"]
}
```
where _build-script_ is the script you want to use to _build_ your project and _args_ is the string of arguments you need to pass your build script in order to process the file. `$file` will be the file you apply the build script on. 

## md4sublime
Usage and output depends on what we want to achieve. 

Options:

```bash
                -h|-help|--help)               No help so far. Seee source code.
                --pdf)                         Convert to PDF                               Generate PDF file from markdown
                -F|--fire*|--Fire*)            Open markdown file in BROWSER = FIREFOX;;    Will show markdown file in Firefox
                -C|--chro*|--Chro*)            Open markdown file in BROWSER = CHROME       Idem, but in Chrome (not yet fully tested)
                --debug)                       DEBUGMODE=true ; KEEPHTML=true ; set -x ;;   Print detail log in sublime console.
                --keep|--keephtml|--keep-html) KEEPHTML=true ;;                             Keep generated html file when rendering in browser.               
                --install) shift; install_this ; exit;;                                     Create sublime builds & install system wide.

```

## md4sublime build scripts
It installs two:
1.- Browser.sublime-build: For viewing markdown in a browser
```JSON
{
  [ "cmd": ["/usr/local/bin/md4sublime", "", "$file"]
}
```
2.- md2pdf.sublime-build: For converting your markdown file into PDF format 
```JSON
{
  [ "cmd": ["/usr/local/bin/md4sublime", "--pdf", "$file"]
}
```

### Installation
```bash
./md4sublime --install
```
Careful: Full system-wide installation will ask for root password. Check the script first to make sure it fits your system.

The default installation directory for the script is in `/usr/local/bin`.

The sublime builds will be installed within `path_to_sublime/Packages/User/`
