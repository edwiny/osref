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
 
 * List env vars
 
 ```
 ls Env:
 ```
 
 * Show contents of var
 
 ```
 cat Env:Path
 # OR
 echo $Env:Path
 # OR
 $Env:Path
 ```
 
* Delete a env var

Just assign empty val:

```
$Env:Foo = ''
```

* Create env vars (process scope)

```
New-Item -Path Env:\Foo -Value 'Bar'
```
OR

```
[Environment]::SetEnvironmentVariable('Foo','Bar')
```

 
 * Make env vars persistent (machine or user scope)
 
Method 1: Add them to $PROFILE
 
 ```
$Env:CompanyUri = 'https://internal.contoso.com'
$Env:Path += ';C:\Tools'
```

Method 2: Set with Machine or User scope

In powershell:
```
[Environment]::SetEnvironmentVariable('Foo', 'Bar', 'Machine')
[Environment]::SetEnvironmentVariable("TEST", "VALUE", "User")

```

Method 3: Control Panel

* Open the System Control Panel.
* Select System.
* Select Advanced System Settings.
* Go to the Advanced tab.
* Select Environment Variables....
* Make your changes.