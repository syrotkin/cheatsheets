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
	
	
## Escape characters

\`t -- inserts a tab character
\`r`n -- inserts a newline

## Working with files

```powershell
    $fileList = Get-ChildItem . # does ls, then each object is really a file, you can query its properties.
    $fileList[0].PSIsContainer  # True if directory
    Set-Location -Path $fileList[0].FullName # does a cd to the directory
```

Iterate through files in a directory:

```powershell
$path = "C:\path_to_directory"

Get-ChildItem $path | ForEach-Object {
    Write-Output "$($_.Name)" 
}
```

Copy file to a different folder:
```powershell
# $_ is the "current" loop variable
Copy-Item -Path $_.FullName -Destination ($path + "\English")
```powershell


## Using .NET types

```powershell
	Add-Type -Path .\UidHelper.dll
	# adds the .NET type, so we can use it from PowerShell code
```	


## Pipeline, foreach

```powershell
	$_ # is the current value in the pipeline
```
Example:
```powershell
		1,2,3 | %{ Write-Output $_ } 
```
	
$_ is also used to access the current error object in an exception, e.g.
```powershell
	Catch 
	{
		ErrorMessage = $_.Exception.Message
	}
```
	
In general:

| %{}  --> is piping each object in a list into some kind of function 
	
	
## Start a process
Start-Process "FilePath"


## Running commands on a remote machine

Invoke-Command - has options to run on a remote machine

-ComputerName <name1> -ScriptBlock {...}

-ComputerName <name1> -FilePath <filepath to ps1 script>
