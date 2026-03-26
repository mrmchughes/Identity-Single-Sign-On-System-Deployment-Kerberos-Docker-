# Identity & Single Sign-On System Deployment (Kerberos / Docker)

Deployed a containerized **Kerberos authentication infrastructure** 
simulating an enterprise SSO environment — a KDC server, client, 
Kerberized OpenSSH server, and Kerberized Apache server — each running 
as a separate Docker container on an isolated bridge network. Users 
authenticate once and access multiple services without re-entering 
credentials.

## Overview

Kerberos solves a real organizational scaling problem: as the number of 
servers and administrators grows, per-server password management becomes 
unmanageable and error-prone. A central KDC lets administrators update 
credentials once and have that change propagate to all services 
automatically. This project implements that architecture end-to-end in 
Docker, validating both SSH and HTTP authentication flows.

**Core concepts demonstrated:**
- Kerberos authentication protocol (AS, TGS, TGT, service tickets)
- Principal and realm management via `kadmin.local`
- Keytab generation and secure distribution to services
- GSSAPI/Kerberos integration with OpenSSH (`sshd_config`)
- `mod_auth_kerb` integration with Apache for HTTP Negotiate auth
- Per-user access control on restricted web directories
- Ticket lifecycle management (`kinit`, `klist`, `kdestroy`)
- Docker Compose multi-container networking with static IPs
- Clock skew diagnosis and ticket lifetime troubleshooting

## Architecture
