# Lab 2 — Storage Access Troubleshooting
**The Storage Nobody Can Access**

## Scenario
A Storage Account was deployed in Azure but nothing could reach it.
Three separate failures all presenting as "access denied" — each caused
by a completely different root cause.

## Problems Found
| # | Problem | Root Cause |
|---|---------|------------|
| 1 | 403 on blob upload despite role assignment | Wrong RBAC role — Storage Account Contributor cannot access blob data. Needs Storage Blob Data Contributor |
| 2 | Private endpoint resolving to public IP | No VNet Link on Private DNS Zone + no DNS Zone Group on private endpoint — private IP never registered |
| 3 | Storage firewall blocking VNet traffic | Subnet had no Microsoft.Storage Service Endpoint + no VNet rule in storage firewall |

## How I Fixed It
- Removed wrong role, assigned Storage Blob Data Contributor using Azure CLI
- Created VNet Link on Private DNS Zone and DNS Zone Group on private endpoint
- Enabled Microsoft.Storage Service Endpoint on subnet, added subnet to storage firewall rules
- Verified end-to-end with successful blob upload at 100%

## Tools Used
PowerShell · Azure CLI · Bicep

## Certification Alignment
AZ-104 — Storage + Networking · AZ-500 — Identity & Data Security

## Evidence
- `Lab2_Incident_Report_INC0087.docx` — full incident report
- `lab2_proof.png` — resources deployed + fixes verified + blob upload 100%
