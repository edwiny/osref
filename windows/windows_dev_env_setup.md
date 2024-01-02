# Notes on Windows Dev Env setups

NOTE:
All shell commands are running as PowerShell.


## Install Windows Terminal

If it's not installed already, install it from the Microsoft Store.



## Install Essentials

```
winget install Git.Git
winget install Notepad++
winget install vscode
```


Set git user name:

```
 git config --global user.email "<EMAIL>"
 git config --global user.name "<NAME>"
 ```
 

Run Notepad++ as Administrator, go to preferences then File Associations, add `.md` under `custom`.


## Create SSH keys


```
ssh-keygen -f $HOME/.ssh/id_rsa_github"
```


Open Notepad++ and save the following config to $HOME/.ssh/config
**NOTE** using the `Encoding` menu, change encoding to `UTF8`
Remember to change path to your user.

```
Host github.com
IdentityFile C:\Users/<USER>/.ssh/id_rsa_github
```

## General Windows config

* Search for "App aliases" and turn off the alias for python.
* Win-E to open explorer, find settings and turn off "hide known file extensions" and other options to taste

* Running scripts from other sources:

```
Set-ExecutionPolicy RemoteSigned
```

Your Documents folder might be automatically synced to OneDrive. To see if it's the case, open a PowerShell and type

```
echo $PROFILE
```

To stop syncing and change your Documents folder to local PC, find OneDrive in system tray, right click and find options. Under *Sync and Backup*
you can change it with the *Manage backup* button.

## PowerShell PROFILE

Create profile with

```
# creates an empty file
ni -Force $PROFILE
```

To find notepad++ path, find it in start menu, right click to open location, then copy path.

First open the profile in legacy notepad:
```
notepad $PROFILE
```

Add the notepad++ path, save, and open a new shell:

```
Set-Alias n "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Notepad++.lnk"
function grep {
  $input | out-string -stream | select-string $args
}
```

## Powershell modules

Optional modules for PowerShell

### ZLocation

In the shell:

```
Install-Module ZLocation -Scope CurrentUser
```


Edit $PROFILE and add:

```
Import-Module ZLocation
```

To use:
* `z`: lists known dirs
* `z pattern`: changes to directory based on pattern

### Oh my posh

```
winget install JanDeDobbeleer.OhMyPosh -s winget
```

Open new terminal:

```
oh-my-posh font install
# select one and note the name
```

In the terminal, press Ctrl-Shift-, and add

```
{
    "profiles":
    {
        "defaults":
        {
            "font":
            {
                "face": "MesloLGM Nerd Font"
            }
        }
    }
}
```

For more info see https://ohmyposh.dev/docs/installation/fonts

List themes:

 `ls "$env:POSH_THEMES_PATH"`
 
 Use one by adding this line to $PROFILE:
 
```
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/atomic.omp.json" | Invoke-Expression
```


## Install python

In PowerShell:
```
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1" 
```
Restart shell

```
 pyenv install 3.12.0
 pyenv global 3.12.0
```




 ## References
 
 https://realpython.com/python-coding-setup-windows/
 
 

