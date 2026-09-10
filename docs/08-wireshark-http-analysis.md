# 08 Wireshark HTTP Analysis

[← Repository overview](../README.md) · [Original PDF report](08-wireshark-http-analysis.pdf)

> Portfolio write-up derived from the original university lab report provided by Smail Mersad. The original report contains screenshots; this GitHub edition uses only results from that report and does not invent additional assets.

**Academic context:** Amar Telidji University, Computer Science / Cybersecurity Engineering, 2025-2026.

## Basic HTTP exchange

The trace showed an HTTP/1.1 GET request and HTTP/1.1 server response. Request headers were inspected for accepted languages, host addressing, and connection behavior. A `200 OK` response confirmed successful retrieval of the requested HTML content.

## Conditional GET and caching

The first request did not contain `If-Modified-Since`, so the server returned the file normally. A later request included a cache-validation timestamp and the server replied:

```text
304 Not Modified
```

No file body was retransmitted, demonstrating how conditional requests reduce unnecessary transfer when a cached copy is still valid.

## Long-document retrieval

A larger document was requested with a single HTTP GET, but the returned content required multiple TCP packets. This reinforces the separation between an HTTP message and the lower-level TCP segments used to carry it.

## Embedded objects

The browser generated separate GET requests for resources referenced by an HTML document, including image objects. The timestamps in the analyzed capture showed the observed resource requests occurring serially in that trace.

## HTTP Basic Authentication

The protected resource initially returned:

```text
401 Unauthorized
```

The browser then resent the request with an `Authorization` header containing Basic credentials encoded in Base64. The lab decoded the captured value and demonstrated that Base64 is encoding, not encryption.

## Security takeaway

Because HTTP Basic credentials can be recovered by anyone able to observe the unencrypted traffic, authentication should be protected with HTTPS/TLS. More broadly, the lab demonstrates how HTTP headers, status codes, caching, object retrieval, authentication, and TCP transport appear in real packet captures.
