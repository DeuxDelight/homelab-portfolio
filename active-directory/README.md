# Active Directory Homelab – Proxmox

## Objective
Build a functional Active Directory environment using Windows Server 2022 and a Windows 11 client to practice domain services, DNS configuration, and identity troubleshooting.

---

## Environment

- **Domain Controller:** Windows Server 2022
- **Client:** Windows 11 Pro
- **Domain:** homelab.local
- **DNS:** AD-integrated DNS on DC
- **Hypervisor:** Proxmox VE

---

## What Was Implemented

- Installed and configured Windows Server 2022
- Promoted the server to a Domain Controller
- Configured DNS for Active Directory
- Created domain users
- Deployed a Windows 11 client VM
- Joined the client to the domain
- Verified domain authentication

---

## Issues Encountered

- DNS resolution timeouts during domain join
- Client authentication falling back to local accounts
- Misleading `nslookup` output related to IPv6 behavior

---

## Root Cause

DNS resolution was impacted by IPv6 preference in a lab environment without full IPv6 routing.  
Once DNS responses were correctly served over IPv4, Windows attempted IPv6 first, resulting in timeouts and confusion during troubleshooting.

---

## Resolution

- Verified DNS service and port bindings
- Confirmed correct A and SRV records
- Adjusted DNS client behavior to prefer IPv4
- Validated DNS resolution from the client
- Successfully joined the client to the domain
- Verified domain login using `whoami`

---

## Verification

- `nslookup homelab.local` resolved correctly
- Domain join completed successfully
- Logged in using a domain user account
- Confirmed domain context via command-line tools

---

## Lessons Learned

- Active Directory is highly dependent on correct DNS configuration
- DNS issues often present as authentication failures
- IPv6 behavior can complicate lab environments if not fully configured

---

## Next Steps

- Implement Group Policy Objects
- Organize users and computers into OUs
- Test policy application and troubleshooting
