# Lab Setup

## Target

OWASP Juice Shop running locally at `http://127.0.0.1:3000`.

## Docker deployment

The lab used a Docker container with a 1 GB Node.js heap limit to reduce memory pressure on the Kali VM:

```bash
docker run -d --name juice-shop -p 3000:3000 -e NODE_OPTIONS=--max-old-space-size=1024 bkimminich/juice-shop
```

## Verification

```bash
docker ps
curl -I http://127.0.0.1:3000
```

## Proxying through Burp

Firefox was configured to use Burp at `127.0.0.1:8080` for HTTP and HTTPS. The Juice Shop target was added to Burp scope before running the scoped crawl/audit.
