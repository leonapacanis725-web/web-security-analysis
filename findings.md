# Web Security Analysis Findings


## HTTP Status Codes
- 200 OK: Successful request.
- 404 Not Found: Requested resource was not found.
- 405 Method Not Allowed: OPTIONS was rejected.

## HTTPS and TLS
- HTTPS connection used TLS 1.3.
- Certificate verification succeeded.
- Certificate matched example.com.
- Server negotiated HTTP/2.

## HTTP vs HTTPS
- HTTP returned HTTP/1.1 200 OK.
- HTTPS returned HTTP/2 200 OK.
- The tested HTTP request was not redirected to HTTPS.

## Security Headers
- X-Frame-Options: SAMEORIGIN
- Referrer-Policy: same-origin
- Cloudflare handled the server response.
