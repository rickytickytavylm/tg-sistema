# TG Web App

Отдельный entry point для Telegram Web App с визуалом мобильного web 1-в-1.

## Что внутри

- `index.html` — копия текущего `frontend/index.html` с абсолютными ссылками на CSS/JS/assets основного web.
- Telegram bridge встроен inline в `index.html`: SDK init, `expand()`, theme colors, Telegram auth через backend.

## Backend

Используется текущий API:

```text
https://web-production-3cb7a.up.railway.app/api
```

Telegram auth endpoint:

```text
POST /api/telegram/auth
```

Payload:

```json
{
  "initData": "...",
  "source": "telegram_webapp"
}
```

Bridge также отправляет заголовок:

```text
X-Sistema-Client: telegram_webapp
```

## Что нужно на backend перед продом

1. Разрешить GitHub Pages origin в CORS.
2. При необходимости сохранять источник входа:
   - `telegram_webapp`
   - `web`
   - `telegram_login_widget`
3. Для админки можно логировать `X-Sistema-Client` или `source` из `/telegram/auth`.

## BotFather

В BotFather нужно указать URL опубликованного GitHub Pages приложения, например:

```text
https://<github-user>.github.io/<repo-or-folder>/
```

Пользователь URL не видит как обычный домен, приложение открывается внутри Telegram.
