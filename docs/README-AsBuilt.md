# Veeam Backup & Replication — As-Built Report

Generates an As-Built document (Word + HTML) of a Veeam VBR server using
AsBuiltReport.

## IMPORTANT — Windows only

This report **cannot run from macOS.** `AsBuiltReport.Veeam.VBR` requires the
`Veeam.Backup.PowerShell` module, which ships *inside the Veeam Backup &
Replication console* and exists only on Windows. It is not on the PowerShell
Gallery and cannot be installed on a Mac. Run everything below **on the VBR
server itself** (or a Windows host with the VBR console installed).

## 1. Launch PowerShell (on the Windows VBR server)

```powershell
# Windows PowerShell 5.1 or PowerShell 7
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted
```

## 2. Install / update the module

```powershell
Install-Module AsBuiltReport.Veeam.VBR -Scope CurrentUser -AllowClobber -SkipPublisherCheck
# later, to update:
Update-Module AsBuiltReport.Veeam.VBR
```

`Veeam.Backup.PowerShell` (v12+) must already be present via the VBR console
install — it is not installed by the command above.

## 3. One-time global config (company info, author)

```powershell
New-AsBuiltConfig      # note the JSON path it prints; reuse it with -AsBuiltConfigFilePath
```

## 4. Generate the As-Built

```powershell
$cred = Get-Credential
New-AsBuiltReport `
  -Report Veeam.VBR `
  -Target localhost `                                       # the VBR server
  -Credential $cred `
  -Format Html,Word `
  -OutputFolderPath "C:\AsBuiltReports" `
  -StyleFilePath "C:\AsBuiltReports\<Company>.Style.ps1" `       # optional company branding (see note)
  -EnableHealthCheck -Verbose
```

## Notes

- `-Target` is usually `localhost` when run on the VBR server; use the VBR host
  name/IP if running from another Windows machine with the console.
- **Company logo / branding:** because this runs on Windows, the cover-page logo
  embeds correctly here (no macOS `System.Drawing` limitation). `-StyleFilePath`
  points to `<Company>.Style.ps1`, pending the logo template. Remove that line until
  the style script exists.
