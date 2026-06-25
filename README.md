# Windows Server RDS Learning Path 20 — Assign Users to the RDS Collection

**Level:** Intermediate · **Module:** 20/70

## Goal
Restrict `RDS-Lab-Desktop` to `CORP\GG-RDS-Users` and prove allowed and denied access.

## Setup
1. Open collection properties in Server Manager.
2. Remove broad default groups such as Domain Users.
3. Add only `CORP\GG-RDS-Users`.
4. Sign out/in after group changes.
5. Test one group member and one user outside the group.
6. Review Broker, Session Host and Security events.

```powershell
Get-RDSessionCollectionConfiguration -CollectionName 'RDS-Lab-Desktop' `
  -ConnectionBroker 'RDS01.corp.lab' | Select-Object CollectionName,UserGroup
Get-ADGroupMember GG-RDS-Users
Get-RDUserSession -ConnectionBroker 'RDS01.corp.lab'
```

## Evidence
Store collection user-group settings, group membership, successful authorized connection, expected unauthorized denial and relevant events under `evidence/`.

## Troubleshooting
If a member is denied, refresh the user's token and verify RDS user-right assignments. If a non-member connects, inspect nested groups and local Remote Desktop Users membership.

## Security
Authorization tests must use normal lab identities; never grant collection access through Domain Admins.

## Rollback
Restore the recorded collection group only when required by the approved design.

## Next
`Windows-Server-RDS-Learning-Path-21-Test-a-Full-Desktop-RDS-Session`
