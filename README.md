# Astro Middleware Bug on Cloudflare Pages

## Problem
Middleware returns `[object Object]` instead of HTML on Cloudflare Pages production.

## Reproduction
1. Clone this repo
2. Install dependencies: `pnpm install`
3. Build and deploy to Cloudflare Pages: `pnpm run deploy`
4. Visit the deployed URL

### Expected behavior
Page should display "Hello World"

### Actual behavior
Page displays `<html><head></head><body>[object Object]</body></html>`

![Screenshot showing [object Object] in browser](./screenshot.png)

### Works correctly
- ✅ Local dev: `pnpm dev`
- ✅ Middleware logs show it's being called
- ✅ Response status is 200
- ❌ Production on Cloudflare Pages

## Environment
- Astro: 5.16.4
- @astrojs/cloudflare: 12.6.12
- wrangler: 4.53.0

## Cloudflare Logs
Middleware is being called successfully:
```json
{
  "outcome": "ok",
  "logs": [
    {
      "message": ["MIDDLEWARE TEST"],
      "level": "log"
    }
  ],
  "event": {
    "response": {
      "status": 200
    }
  }
}
```

✅ Middleware executes  
✅ Response status: 200  
❌ Response body is broken


## Solution (Temporary Workaround)
This issue is tracked in [withastro/astro#14511]([ссылка](https://github.com/withastro/astro/issues/14511)).
