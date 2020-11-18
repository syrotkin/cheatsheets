- [OS Interaction](#os-interaction)
  * [Determine installed PowerShell version](#determine-installed-powershell-version)
  * [Run a Windows executable](#run-a-windows-executable)
  * [Setting environment variables from the command line](#setting-environment-variables-from-the-command-line)
  * [Start a process](#start-a-process)
  * [Running commands on a remote machine](#running-commands-on-a-remote-machine)
- [Regular expressions with captures:](#regular-expressions-with-captures-)
- [Escape characters](#escape-characters)
- [Working with files](#working-with-files)
  * [Get content](#get-content)
  * [Tail](#tail)
  * [Working with file objects](#working-with-file-objects)
  * [Iterate through files in a directory:](#iterate-through-files-in-a-directory-)
  * [Copy file to a different folder:](#copy-file-to-a-different-folder-)
  * [Write to a file](#write-to-a-file)
- [Using .NET types](#using-net-types)
- [Pipeline, foreach](#pipeline--foreach)
- [Sorting](#sorting)
- [Arrays](#arrays)
  * [Create and populate](#create-and-populate)
- [Hash tables:](#hash-tables-)
  * [Create and populate:](#create-and-populate-)
  * [Check for keys:](#check-for-keys-)
  
<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## OS Interaction

### Determine installed PowerShell version
```powershell
$PSVersionTable.PSVersion
```

### Run a Windows executable

```powershell
& .\myProgram.exe
```

### Setting environment variables from the command line
To set the variable in the CMD shell, do the following:

    set OSY=Syrotkin    // this will change the variable in the current window

    setx OSY "Syrotkin" /m    // this will change the variable in other windows

From PowerShell:
```powershell
Set-Item -Path env:DB2CLP -value "**$$**"
# this works and does not do the funny $$ conversion
```

Otherwise, try this, using .NET libraries:

```powershell
[Environment]::SetEnvironmentVariable("OSY", "Machine1", "Machine")
# sets the environment variable to "Machine1" in the "Advanced system settings" (where I would normally set Environment variables)
	
[Environment]::SetEnvironmentVariable("OSY", "User1", "User")
# sets the environment variable to "User1" in subsequent PowerShell and cmd windows
	
[Environment]::SetEnvironmentVariable("OSY", "Process1", "Process")
# sets the environment variable OSY to  "Process1" in the current window (only)
```

### Start a process
Start-Process "FilePath"


### Running commands on a remote machine

`Invoke-Command` - has options to run on a remote machine

`-ComputerName <name1> -ScriptBlock {...}`

`-ComputerName <name1> -FilePath <filepath to ps1 script>`


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

### Get content

```powershell
$file = Get-Content 'path_to_file'
foreach ($line in $file) {
	# do something
}
```

### Tail

```powershell
Get-Content myFile.txt -Tail 10
```

### Working with file objects

```
$fileList = Get-ChildItem . # does ls, then each object is really a file, you can query its properties.
$fileList[0].PSIsContainer  # True if directory
Set-Location -Path $fileList[0].FullName # does a cd to the directory
```

### Iterate through files in a directory:

```powershell
$path = "C:\path_to_directory"

Get-ChildItem $path | ForEach-Object {
    Write-Output "$($_.Name)" 
}
```

### Copy file to a different folder:
```powershell
# $_ is the "current" loop variable
Copy-Item -Path $_.FullName -Destination ($path + "\English")
```

### Write to a file
Replace content of a file:
```powershell
Set-Content -Path $outPath -Value 'some value'
```

Append to a file:
```powershell
Add-Content -Path $outPath -Value 'some value'
```

## Using .NET types
```powershell
Add-Type -Path .\UidHelper.dll
# adds the .NET type, so we can use it from PowerShell code
```	


## Pipeline, foreach
`$_` is the current value in the pipeline

Example:
```powershell
1,2,3 | %{ Write-Output $_ } 
```
	
`$_` is also used to access the current error object in an exception, e.g.
```powershell
Catch 
{
	ErrorMessage = $_.Exception.Message
}
```
	
In general:

`| %{}`  --> is piping each object in a list into some kind of function 
	
A C#-like foreach exists in PowerShell, too:
```powershell
foreach ($item in $array) {
	# Do something
}
```

## Sorting
```powershell
$set = $set | Sort-Object
```

## Arrays
### Create and populate
```powershell
$array = @()
$array += 1
$array += 2
# OR:
$array = 1, 2, 3
```

## Hash tables:
### Create and populate:
```powershell
$hashTable = @{}
$hashTable["foo"] = "bar"
```
### Check for keys:
```powershell
if ($hashTable.ContainsKey("foo")) {... } # Same as .NET
```
