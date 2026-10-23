#!/usr/bin/env bash
# Apply proxy_ssl_server_name globally on Nginx (HestiaCP)
set -euo pipefail

if [[ $EUID -ne 0 ]]; then
  echo "Run as root: sudo $0"
  exit 1
fi

echo -e "proxy_ssl_server_name on;\nproxy_ssl_name \$host;" \
  | tee /etc/nginx/conf.d/fixssl.conf

nginx -t
systemctl restart nginx

echo "OK — global SNI applied."
