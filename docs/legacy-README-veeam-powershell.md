# veeam-powershell

PowerShell automation scripts for Veeam Backup & Replication infrastructure.

## Contents

| Script | Purpose |
|--------|---------|
| `get-vbr-job-status.ps1` | Report on Veeam backup job status |

## Prerequisites

- Veeam Backup & Replication installed (VBR 11+ or 12+)
- Veeam PowerShell Toolkit (included with VBR installation)

```powershell
# VBR 11 and earlier
Add-PSSnapin VeeamPSSnapin

# VBR 12+ loads automatically
Connect-VBRServer -Server $vbrServer -Credential (Get-Credential)
```

## CI/CD

All PRs are validated by PSScriptAnalyzer, secret scan, and header compliance checks.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Owner

humbledgeeks-allen | [HumbledGeeks.com](https://humbledgeeks.com)
