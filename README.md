# Web Security Analysis

## Objective

Analyze basic HTTP and HTTPS behavior using `curl`. Compare response status codes, transport security, certificate verification, protocol negotiation, redirect behavior, and selected security headers.

## Environment & Tools

- Linux command-line environment
- `curl` for making HTTP and HTTPS requests and inspecting server responses
- Test target: `example.com`
- Evidence file: `findings.md`

The results document observations from the test requests at the time they were made. Server configuration and responses can change.

## Methodology & Commands

1. Send requests to the test host over HTTP and HTTPS using `curl`.
2. Compare the returned HTTP status codes and protocol versions.
3. Review the HTTPS connection details, including negotiated TLS version and certificate verification result.
4. Check whether the HTTP request is redirected to HTTPS.
5. Review security-related response headers returned by the server.
6. Record the observations in `findings.md` and distinguish observed behavior from broader security conclusions.

The project identifies `curl` as the command-line tool used. The README does not add unverified command flags or claim a particular request sequence beyond the recorded findings.

## Key Findings

- The tested requests returned HTTP 200 OK for both HTTP and HTTPS.
- The HTTP request used HTTP/1.1; the HTTPS request negotiated HTTP/2.
- The HTTPS connection used TLS 1.3.
- Certificate verification succeeded, and the certificate matched `example.com`.
- The tested HTTP request was not redirected to HTTPS.
- The sample response included `X-Frame-Options: SAMEORIGIN` and `Referrer-Policy: same-origin`.
- The server response was handled by Cloudflare.
- Other observed responses included 404 Not Found and 405 Method Not Allowed; the OPTIONS request was rejected.

These findings describe the responses observed during this exercise. A successful HTTPS connection does not by itself establish that an entire website is secure, and the absence of an HTTP-to-HTTPS redirect applies only to the tested request.

## Remediation / Security Takeaway

- Configure HTTP requests to redirect to HTTPS so visitors do not remain on an unencrypted connection.
- Use a valid TLS certificate and current TLS configuration; verify certificate identity and trust during testing.
- Review security headers against the application's requirements. Headers such as `X-Frame-Options` and `Referrer-Policy` help address specific browser-side risks but are not a complete security control.
- Investigate unexpected status codes and confirm that unsupported HTTP methods are rejected intentionally.
- Repeat checks across relevant paths and endpoints; a single request is only a limited snapshot of server behavior.

## Project Files

- `findings.md` — Recorded HTTP status, TLS, protocol, redirect, and response-header observations.

## Disclaimer

This project is a basic defensive web-security learning exercise using command-line requests. Findings reflect the test responses recorded in the project and do not represent a comprehensive assessment or penetration test of the target.
