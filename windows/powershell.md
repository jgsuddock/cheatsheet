# Powershell

### General Commands

```powershell
# Command Documentation
Get-Help
Get-Help -Category {Cmdlet}                    # Only show Cmdlet results

# Gets list of available commands that match
Get-Command
Get-Command -CommandType {Cmdlet}              # Only show Cmdlet results

# Delete Files
Remove-Item -Path {Path}                       # Dir or File Path (optional)
Remove-Item -Recurse                           # Recursive search
Remove-Item -Include {*.txt, *.greg}           # Deletes only the *.txt files
Remove-Item -Exclude {*.txt}                   # Ignore the *.txt files

# Show Items In Directory
Get-ChildItem -Path {Path}                     # Dir or File Path (optional)
Get-ChildItem -Force                           # Include Hidden Items
Get-ChildItem -Recurse                         # Recurse search
Get-ChildItem -Include {*.txt, *.greg}         # Only show *.txt files
Get-ChildItem -File                            # Only files
Get-ChildItem -ErrorAction SilentlyContinue    # Ignore Errors
Get-ChildItem | Where-Object {                 # Check results from specific date
    $_.LastWriteTime -ge (Get-Date -Year 2019 -Month 12 -Day 13)
}

# Watch Log File
Get-Content -Path {Path}          # File Path (optional)
Get-Content -Wait                 # Wait for more lines to be written to file
Get-Content -Tail {Count}         # Shows last {count} lines

# Run Command On Remote Server
Invoke-Command -ComputerName                      # <Name of Remote Computer>, (<Name of Remote Computer 2>)?...
Invoke-Command -Credential                        # 'DOMAIN\username'  Tells the script to run as administrator on the server.
Invoke-Command -ScriptBlock                       # Command to be ran on the remote computer. Put your command inside curly braces i.e.
Invoke-Command -ScriptBlock { Get-Process *py* }  # Runs Get-Process on remote computer.
Invoke-Command -FilePath                          # Path to script on local PC to be ran on each of the servers

# Print command output to file and to screen
{Command} | Tee-Object -FilePath {".\log.txt"}

# DNS Lookup
Resolve-DnsName -Name {www.google.com}               # Lookup information about a given DNS name
Resolve-DnsName -Name {www.google.com} -Type CNAME   # Only looks up CNAME entries for a given DNS name

# Credential Management
$cred = Get-Credential
$cred = Get-Credential -UserName $Env:USERNAME
Write-Output $cred.UserName                            # Prints Entered Username
Write-Output $cred.Password                            # Prints SecureString Object
Write-Output $cred.GetNetworkCredential().Password     # Prints Entered Unencrypted Password
```

### Folder Permission Audit

```powershell
param (
    [string]$path = ".",
    [switch]$automated = $false
)

$FolderPath = Get-ChildItem -Directory -Path $path -Recurse -Force
$Report = @()
Foreach ($Folder in $FolderPath) {
    $Acl = Get-Acl -Path $Folder.FullName
    foreach ($Access in $acl.Access)
        {
            $Properties = [ordered]@{'FolderName'=$Folder.FullName;'AD Group or User'=$Access.IdentityReference;'Permissions'=$Access.FileSystemRights;'Inherited'=$Access.IsInherited}
            $Report += New-Object -TypeName PSObject -Property $Properties
        }
}

$fileName = "{0}-{1}{2}" -f "FolderPermissions", (Get-Date -Format "yyyy-MM-dd-HH.mm.ss"), ".csv"
$outputFile = Join-Path $PSScriptRoot $fileName
$Report | Export-Csv -Path $outputFile
If (-Not $automated)
{
    Invoke-Item $outputFile
}
```

### Get Computer Name PS1

```powershell
Function Pause ($Message = "Press any key to continue...") {
   # Check if running in PowerShell ISE
   If ($psISE) {
      # "ReadKey" not supported in PowerShell ISE.
      # Show MessageBox UI
      $Shell = New-Object -ComObject "WScript.Shell"
      $Button = $Shell.Popup("Click OK to continue.", 0, "Hello", 0)
      Return
   }

   $Ignore =
      16,  # Shift (left or right)
      17,  # Ctrl (left or right)
      18,  # Alt (left or right)
      20,  # Caps lock
      91,  # Windows key (left)
      92,  # Windows key (right)
      93,  # Menu key
      144, # Num lock
      145, # Scroll lock
      166, # Back
      167, # Forward
      168, # Refresh
      169, # Stop
      170, # Search
      171, # Favorites
      172, # Start/Home
      173, # Mute
      174, # Volume Down
      175, # Volume Up
      176, # Next Track
      177, # Previous Track
      178, # Stop Media
      179, # Play
      180, # Mail
      181, # Select Media
      182, # Application 1
      183  # Application 2

   Write-Host -NoNewline $Message
   While ($KeyInfo.VirtualKeyCode -Eq $Null -Or $Ignore -Contains $KeyInfo.VirtualKeyCode) {
      $KeyInfo = $Host.UI.RawUI.ReadKey("NoEcho, IncludeKeyDown")
   }
}

Write-Host $env:ComputerName
Pause("Press any key to copy to clipboard...")
Set-Clipboard -Value $env:ComputerName
Exit
```

### Get IP Address

```powershell
Function Pause ($Message = "Press any key to continue...") {
    # Check if running in PowerShell ISE
    If ($psISE) {
       # "ReadKey" not supported in PowerShell ISE.
       # Show MessageBox UI
       $Shell = New-Object -ComObject "WScript.Shell"
       $Button = $Shell.Popup("Click OK to continue.", 0, "Hello", 0)
       Return $null;
    }

    $Ignore =
       16,  # Shift (left or right)
       17,  # Ctrl (left or right)
       18,  # Alt (left or right)
       20,  # Caps lock
       91,  # Windows key (left)
       92,  # Windows key (right)
       93,  # Menu key
       144, # Num lock
       145, # Scroll lock
       166, # Back
       167, # Forward
       168, # Refresh
       169, # Stop
       170, # Search
       171, # Favorites
       172, # Start/Home
       173, # Mute
       174, # Volume Down
       175, # Volume Up
       176, # Next Track
       177, # Previous Track
       178, # Stop Media
       179, # Play
       180, # Mail
       181, # Select Media
       182, # Application 1
       183  # Application 2

    Write-Host -NoNewline $Message
    While ($null -eq $KeyInfo.VirtualKeyCode -Or $Ignore -Contains $KeyInfo.VirtualKeyCode) {
       $KeyInfo = $Host.UI.RawUI.ReadKey("NoEcho, IncludeKeyDown")
    }
    Return $KeyInfo.VirtualKeyCode
 }

 # Get-NetIPConfiguration
 $config = Get-NetIPAddress -AddressFamily IPv4 -AddressState Preferred | Where-Object { -not $_.InterfaceAlias.StartsWith("Loopback") -and -not $_.InterfaceAlias.StartsWith("vEthernet") }
 $config | Format-List InterfaceIndex, InterfaceAlias, IPAddress
 $pressed_key = Pause
 If ($null -ne $pressed_key)
 {
     Write-Host ""
     $selection = $pressed_key - 97
     $count = ($config | Measure-Object).count
     If ($selection -lt $count -and $selection -ge 0)
     {
         Set-Clipboard -Value $config[$selection].IPv4Address
         Write-Host "Copied" $config[$selection].IPv4Address
     }
 }
 Exit
```

### Map Drives

```powershell
$i = 3
while ($True)
{
    $error.clear()
    $MappedDrives = Get-SmbMapping | Where-Object -Property Status -Value Unavailable -EQ | Select-Object LocalPath,RemotePath
    foreach ($MappedDrive in $MappedDrives)
    {
        try {
            New-SmbMapping -LocalPath $MappedDrive.LocalPath -RemotePath $MappedDrive.RemotePath -Persistent $True
        } catch {
            Write-Host "There was an error mapping $MappedDrive.RemotePath to $MappedDrive.LocalPath"
        }
    }
    $i = $i - 1
    if ($error.Count -eq 0 -Or $i -eq 0) { break }

    Start-Sleep -Seconds 30
}
```

### Pause

```powershell
Function Pause ($Message = "Press any key to continue...") {
   # Check if running in PowerShell ISE
   If ($psISE) {
      # "ReadKey" not supported in PowerShell ISE.
      # Show MessageBox UI
      $Shell = New-Object -ComObject "WScript.Shell"
      $Button = $Shell.Popup("Click OK to continue.", 0, "Hello", 0)
      Return
   }

   $Ignore =
      16,  # Shift (left or right)
      17,  # Ctrl (left or right)
      18,  # Alt (left or right)
      20,  # Caps lock
      91,  # Windows key (left)
      92,  # Windows key (right)
      93,  # Menu key
      144, # Num lock
      145, # Scroll lock
      166, # Back
      167, # Forward
      168, # Refresh
      169, # Stop
      170, # Search
      171, # Favorites
      172, # Start/Home
      173, # Mute
      174, # Volume Down
      175, # Volume Up
      176, # Next Track
      177, # Previous Track
      178, # Stop Media
      179, # Play
      180, # Mail
      181, # Select Media
      182, # Application 1
      183  # Application 2

   Write-Host -NoNewline $Message
   While ($KeyInfo.VirtualKeyCode -Eq $Null -Or $Ignore -Contains $KeyInfo.VirtualKeyCode) {
      $KeyInfo = $Host.UI.RawUI.ReadKey("NoEcho, IncludeKeyDown")
   }
}

Pause
Exit
```

### Remote Selector

```powershell
$Servers = @(
    [PSCustomObject]@{Type = 'SSH'; Name = 'SERVERNAME'; Domain = 'SERVER_DOMAIN'}
    [PSCustomObject]@{Type = 'PS'; Name = 'SERVERNAME'; Domain = 'SERVER_DOMAIN'}
)

$GridArguments = @{
    OutputMode = 'Single'
    Title      = 'Please select a server and click OK'
}

$Server = $Servers | Out-GridView @GridArguments

$Session = $null
if ($Server)
{
    if ($Server.Type -eq 'SSH') {
        Write-Output "Connecting to $($Server.Name) at $($Server.Domain)"
        Write-Output "ssh $Env:USERNAME@$($Server.Domain).domain.com"
        ssh "$Env:USERNAME@$($Server.Domain).domain.com"
    }
    else {
        $Session = Get-PSSession | Where-Object { $_.ComputerName -eq $Server.Domain } | Sort-Object -Property Id -Descending
        if (($Session | Measure-Object).Count -gt 0) {
            Write-Host "Found Session"
            $Session = $Session[0]
        }
        else {
            Write-Host "New Session"
            $Session = New-PSSession -ComputerName $Server.Domain -Credential 'DOMAIN\username'
        }
        $host.ui.RawUI.WindowTitle = "PS ($($Server.Domain)) - [$($Session.Id)]"
        Write-Host "Connecting to PS Session ID: $($Session.Id)"
        $Session | Enter-PSSession
        Write-Host ""
        Write-Host "Session Help:"
        Write-Host "    * To stop the session:                    > exit"
        Write-Host "    * To remove this session after exiting:   > Remove-PSSession -Id $($Session.Id)"
        Write-Host "    * To see other sessions available:        > Get-PSSession"
        Write-Host ""
    }
}
```

### Keyboard Shortcuts