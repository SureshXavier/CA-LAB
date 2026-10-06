# Certificate Authority Practice Lab

A hands-on **two-tier PKI** built from scratch: an air-gapped **Offline Root CA**, an **Enterprise Subordinate CA** integrated with Active Directory, HTTP CRL/AIA publication through IIS, certificate **auto-enrollment** via Group Policy, and a fully tested **issue → trust → revoke → verify** lifecycle.

**Live portfolio:** https://sureshxavier.github.io/CA-Lab/

## Lab Components

| Machine | Role | Key configuration |
|---|---|---|
| ROOT-CA | Standalone Root CA (offline) | RSA 4096, SHA256, 15-year validity, CRL period in years, not domain-joined |
| DC01 | Domain Controller + DNS | Forest `lab.local`, static IP, GPO auto-enrollment |
| SUB-CA | Enterprise Subordinate (issuing) CA | RSA 2048, SHA256, signed by ROOT-CA, IIS for HTTP CDP/AIA, `LabUserCert` template |
| CLIENT01 | Domain client | Auto-enrolled user certificate, revocation verified over HTTP |

## What Was Done

1. Built the offline Root CA (Standalone, 4096-bit, 15 years) and published the first CRL
2. Built the domain controller and created the `lab.local` forest
3. Prepared the Subordinate CA, joined it to the domain, and generated its certificate request
4. Performed the signing ceremony across the air gap using a VMware shared folder
5. Installed the signed certificate and published the Root CA into Active Directory
6. Set up CRL and AIA publication over HTTP using IIS
7. Created the `LabUserCert` template and enabled auto-enrollment through Group Policy
8. Tested the full lifecycle: issue, revoke, publish CRL, verify `CRYPT_E_REVOKED` from the client

## Issues & Resolutions

Six issues were hit and fixed (AD DS prerequisites, DNS misconfiguration on domain join, UNC path limits in CMD, a false-alarm install error, CA service startup against an offline issuer, and HTTP CDP name resolution). Full cause and fix for each are on the live portfolio.

## Skills Demonstrated

CA hierarchy design · Offline root discipline · CDP/AIA configuration · Enterprise CA + Active Directory · Certificate templates · Auto-enrollment (GPO) · CRL publishing and revocation · Troubleshooting

## Repository Structure

```
CA-Lab/
├── index.html   # the portfolio page (served by GitHub Pages)
└── README.md    # this file
```

## Contact

**D. Suresh Xavier** · Security Operations Engineer · xavierreivax15@gmail.com
