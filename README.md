# veeam-vbr

Reusable **Veeam Backup & Replication** reporting automation. Read-only.

## Contents

| Path | Language | What it does | Effect |
|---|---|---|---|
| `powershell/get-vbr-job-status.ps1` | PowerShell (legacy `VeeamPSSnapin` snap-in) | Backup job results and repository capacity report | read-only |
| `ansible/veeam-job-status.yml` | Ansible (`uri`, VBR REST API) | Backup job status report | read-only |
| `docs/README-AsBuilt.md` | — | How to produce a VBR as-built report (Windows only; requires the VBR console module) | — |
| `docs/legacy-README-*.md` | — | Original per-repository READMEs | — |

## Prerequisites

- PowerShell on a Windows host with the Veeam Backup & Replication console installed (not on the PowerShell Gallery); `Connect-VBRServer` with prompted credentials. The script loads the legacy `VeeamPSSnapin`; Veeam v12+ replaced the snap-in with the `Veeam.Backup.PowerShell` module, so the load block needs updating for v12+ (known stale reference).
- Ansible with vault-provided REST credentials; VBR REST API enabled.

## Environment-specific configuration

Server names and credentials are supplied at run time. Deployment runbooks and screenshots from
the previous repositories are kept outside this repository.

## Credentials and safety

No credentials are stored in this repository. PowerShell scripts prompt (`Get-Credential`) or read
environment variables; Ansible playbooks expect an Ansible Vault (`--ask-vault-pass`) providing the
`vault_*` variables named in `group_vars`. Never commit vault files, Clixml exports or `.env` files
(see `.gitignore`). Run output (reports, CSV, logs) is generated content and is git-ignored; keep it
outside the repository.

## Provenance

Consolidated from previous local automation repositories during the 2026 LabOps repository
cleanup. This repository starts with a fresh history; earlier history is retained locally only.
