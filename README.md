# Telegram Bot on Railway

## Railway variables

Set these variables in Railway service settings:

- `BOT_TOKEN` - token from BotFather.
- `ADMIN_ID` - your Telegram numeric user id.
- `API_KEY` - a long random secret shared with the PC client.
- `WEBHOOK_SECRET` - optional; if omitted, it is derived from `API_KEY`.

Railway injects `PORT` automatically. After enabling public networking, Railway also exposes `RAILWAY_PUBLIC_DOMAIN`, which the bot uses to configure the Telegram webhook. If needed, set `PUBLIC_URL` manually, for example `https://your-app.up.railway.app`.

## Start command

The Railway start command is stored in `railway.json`:

```bash
gunicorn telegram_bot:app --bind 0.0.0.0:$PORT --workers 1 --timeout 120
```

The service also exposes `/health` for Railway healthchecks.

## Local run

Create a local `.env` from `.env.example` or set the variables in your shell, then run:

```bash
python telegram_bot.py
```

Without `PUBLIC_URL` or `RAILWAY_PUBLIC_DOMAIN`, the bot uses Telegram polling locally.
