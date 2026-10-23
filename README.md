# hestia-proxy-ssl-fix

Fixes for proxy (SNI) and SSL issues on HestiaCP servers running
Nginx + Apache as reverse proxy, with Let's Encrypt and multiple domains.

## Environment

- HestiaCP 1.9.x
- Nginx (frontend, ports 80/443)
- Apache2 (backend, ports 8080/8443)
- PHP-FPM
- Let's Encrypt
- (Optional) VitalPBX installed on the same server

## Documented issues

1. [VitalPBX capturing all domains](01-vitalpbx-capturing-all-domains.md)
2. [Invalid webmail certificate](02-webmail-certificate-invalid.md)
3. [DNS verification fails on Let's Encrypt issuance](03-dns-verification-fails.md)

## Scripts

- `scripts/fix-sni-global.sh` — applies `proxy_ssl_server_name` globally
- `scripts/rebuild-all-domains.sh` — rebuilds all web domains for all users

## Usage

Always run Hestia commands as root:

```bash
sudo -i
