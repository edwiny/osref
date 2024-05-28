# PowerShell notes


## Get current user

`$Env:UserName`

## Sourcing a file for env vars or functions

```
. .\thefile.ps1
```

Note it needs the '.\'. Also do not give it a `.env` suffix.

## Writing to console

Write to stdout but not to pipeline (e.g. piped commands won't see this)

`Write-Host "hello world"`