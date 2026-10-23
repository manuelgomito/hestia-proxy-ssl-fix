# Issue: VitalPBX appearing on all domains

## Symptom

Every domain on the server showed the VitalPBX login page,
regardless of the `server_name` configured in Nginx.

## Diagnosis

- Nginx listening correctly on 80/443
- Apache listening on 8080/8443 (backend)
- Apache VirtualHosts correctly configured per domain
- Nginx templates already contained `proxy_ssl_server_name on;`
- **Generated per-domain config files did NOT contain the SNI directive**

## Root cause

Known HestiaCP bug after the Apache 2.4.64 update:
Nginx did not send SNI when proxying SSL to Apache.
Apache could not distinguish the domain and fell back to the
first loaded VirtualHost (VitalPBX).

## Fix

1. Ensure the Nginx template contains:
   ```nginx
   proxy_ssl_server_name on;
   proxy_ssl_name $host;
