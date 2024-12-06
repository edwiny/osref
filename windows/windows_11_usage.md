# Windows 11 usage tips



## Window management

* Win-Z - bring up window tiling thing
* Win-Z + arrow keys: move active window
* Alt-Ctrl: cycle windows based on order of opening

Multiple desktops:

* Win+Tab: manage and create new desktops
* Ctrl-Win+Arrow keys: switch desktops

## Shortcuts


* Quick access to admin functions: right click on Start Menu
* Ctrl-Shift-Esc: open Task Manager
*  Win-A: quick settings for wifi, sound settings, music



## Command line tricks

* Copy to clipboard

```
clip < path_to_file
cat path_to_file | clip
```

* Get an application's full path:

```
 (Get-Command notepad).Source
 ```
 
 
 
 ## Environment variables
 
 Env vars have 3 scopes:
 * Process - default if you create new vars in the shell
 * User
 * Machine (aka system)

### Using Powershell

* List

```
Get-ChildItem Env:
# OR
dir Env:
```
* Set

```
Set-Item -Path Env:\BB_TOKEN -Value 'BAR'
# OR
$Env:BB_TOKEN = "value"
```

* Get
```
Get-Item -Path Env:\Foo*
# OR
cat $Env:Foo
```

* Delete

Just assign empty val:

```
$Env:Foo = ''
```


### Set with Machine scope

In powershell:
```
[Environment]::SetEnvironmentVariable('Foo', 'Bar', 'Machine')
```

### Set permanently with Control Panel

* Open the System Control Panel.
* Select System.
* Select Advanced System Settings.
* Go to the Advanced tab.
* Select Environment Variables....
* Make your changes.
