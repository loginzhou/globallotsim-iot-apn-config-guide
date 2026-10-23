# IoT SIM APN Configuration Guide for Cellular Modules

APN setup, AT commands and network registration checks for M2M modules and industrial routers using a [Quanqiu IoT](https://www.globallotsim.com) Global IoT SIM.

> **APN:** most Quanqiu IoT SIMs use the APN `mobile` with no username or password. Some plans and private-network projects use a different APN. Always use the APN printed on the delivery sheet that came with your SIMs, and ask your account manager if it is missing.

## Quick links
- Website: [globallotsim.com](https://www.globallotsim.com)
- Service: Global IoT SIM cards, eSIM profiles and a connectivity management platform (CMP) for B2B device fleets.

---

## 1. Quectel modules (EC25, EG25-G, BG96, BG95)

```at
AT+CGDCONT=1,"IP","mobile"     // define PDP context 1 with the APN
AT+QICSGP=1,1,"mobile","","",1 // TCP/IP context: IPv4, APN, no user/password
AT+COPS=0                      // automatic operator selection
AT+CEREG?                      // LTE / LTE-M / NB-IoT registration: ,1 home or ,5 roaming
AT+CREG?                       // 2G/3G registration
AT+QIACT=1                     // activate the context
AT+QIACT?                      // show the assigned IP address
```

A Global IoT SIM normally registers as **roaming** (`,5`). That is expected and not an error.

## 2. SIMCom modules (SIM7600, SIM7000, A7670)

```at
AT+CGDCONT=1,"IP","mobile"
AT+COPS=0
AT+CEREG?
AT+CGACT=1,1                   // activate PDP context 1
AT+CGPADDR=1                   // show the assigned IP address
```

## 3. Industrial routers

Set the APN in the router's cellular or WAN settings:

| Field | Value |
|-------|-------|
| APN | `mobile` (or the APN on your delivery sheet) |
| Username / password | leave empty |
| Authentication | None |
| PDP type | IPv4 |
| Roaming | **Enabled**, since a Global IoT SIM attaches as a roaming subscriber |

## Troubleshooting

| Symptom | Check |
|---------|-------|
| Registered but no data | APN spelling; data roaming enabled; SIM active in the CMP |
| `+CEREG: 0,0` or `0,3` (not registered / denied) | Antenna and coverage; module bands match the country; SIM not suspended |
| Worked, then stopped | Data limit reached or SIM suspended; check usage in the CMP |

For guides on choosing IoT SIM plans by country and device type, see [globallotsim.com](https://www.globallotsim.com).

## Related tools and guides

- [IoT data usage calculator](https://www.globallotsim.com/iot-data-usage-calculator/) — estimate monthly data per device and per fleet ([source](https://github.com/loginzhou/iot-data-usage-calculator))
- [IoT SIM for GPS trackers: 30 MB plans, pooled data and APN setup](https://www.globallotsim.com/gps-tracker-sim/)
- [2G and 3G shutdowns for GPS trackers](https://www.globallotsim.com/iot-sim-for-gps-trackers-after-2g-3g-shutdown-migration-and-sms-continuity/) — finding 2G-only units, LTE Cat-1/LTE-M replacements, SMS on LTE

## License

MIT
