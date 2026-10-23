# Global B2B IoT SIM & eSIM APN Configuration Guide

Official APN setup guides, AT commands, and network registration instructions for M2M hardware modules and industrial routers powered by [globallotsim](https://www.globallotsim.com).

## Quick Links
- **Official Website**: [globallotsim.com](https://www.globallotsim.com)
- **Service**: B2B Global IoT SIM Cards, eSIM Profiles, and M2M Connectivity Management Portal.

---

## 1. Quectel LTE/M2M Modules (EC25, BG96, EG25-G)
Set APN parameters using standard AT commands:

```at
AT+CGDCONT=1,"IP","globallotsim"
AT+COPS=0
