#!/usr/bin/env bash
# Rebuild all web domains for all Hestia users
set -euo pipefail

if [[ $EUID -ne 0 ]]; then
  echo "Run as root: sudo $0"
  exit 1
fi

for user in $(v-list-users plain | cut -f1); do
  echo ">>> Rebuilding $user"
  v-rebuild-web-domains "$user" yes || \
    echo "  ! failed for $user (check permissions)"
done

systemctl restart nginx
systemctl restart apache2
echo "OK — all domains rebuilt."
