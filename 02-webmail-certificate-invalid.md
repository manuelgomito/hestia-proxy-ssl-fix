# Issue: Invalid webmail certificate

## Symptom

`https://webmail.domain.com` showed:
`ERR_CERT_AUTHORITY_INVALID`

## Diagnosis

```bash
echo | openssl s_client -connect webmail.domain.com:443 \
  -servername webmail.domain.com 2>/dev/null \
  | openssl x509 -noout -subject -issuer -dates
