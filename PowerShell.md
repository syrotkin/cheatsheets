## Setting environment variables from the command line
to set the variable  in the CMD shell, do the following:

    set OSY=Syrotkin    // this will change the variable in the current window

    setx OSY "Syrotkin" /m    // this will change the variable in other windows

From PowerShell:

```powershell
    [Environment]::SetEnvironmentVariable("OSY", "Machine1", "Machine")
    # sets the environment variable to "Machine1" in the "Advanced system settings" (where I would normally set Environment variables)
    	
    [Environment]::SetEnvironmentVariable("OSY", "User1", "User")
    # sets the environment variable to "User1" in subsequent PowerShell and cmd windows
    	
    [Environment]::SetEnvironmentVariable("OSY", "Process1", "Process")
    # sets the environment variable OSY to  "Process1" in the current window (only)
```

## Regular expressions with captures:

```powershell
    $pattern = '.+\(EGRID: (CH\d{12}), GF: (A\d\d-\d{6})\).+'
    if ($line -match $pattern) {
    	# Automatic $Matches variable is set.
    	Write-Output $Matches[0] # Writes the entire matched line
    	Write-Output "$($Matches[1])_$($Matches[2])"  # writes <EGRID>_<GF>
    }
```
	
	
## Special characters

\`t -- inserts a tab character


## Working with files

```powershell
    $fileList = Get-ChildItem . # does ls, then each object is really a file, you can query its properties.
    $fileList[0].PSIsContainer  # True if directory
    Set-Location -Path $fileList[0].FullName # does a cd to the directory
```