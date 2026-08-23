# Cloudflare Worker

Скрипт для Cloudflare Worker, перенесённый из [tg-ws-proxy](https://github.com/Flowseal/tg-ws-proxy) (`docs/CfWorker.md`).
Worker принимает WebSocket-подключение на `/apiws?dst=<host>` и прозрачно
проксирует его в TCP-соединение с `dst:443` — то есть работает как раз тот
эндпоинт, к которому обращается клиент (`src/cfproxy.rs`, `cf_connect_domain`)
при подключении через CloudFlare.

## Деплой

1. Зарегистрируйтесь / войдите на [dash.cloudflare.com](https://dash.cloudflare.com/).
2. `Compute` → `Workers & Pages` → `Create application` → `Start with Hello World!` → `Deploy`.
3. `Edit code` — вставьте содержимое [`worker.js`](./worker.js) вместо шаблонного кода.
4. `Deploy`.
5. Скопируйте выданный домен (вида `random-symbols-1234.username.workers.dev`).

## Использование в приложении

Готовый домен указывается в настройках приложения: `CloudFlare CDN` → свой домен
(поле `customCfDomain`, тумблер `customCfDomainEnabled` в `SettingsTab.kt`).
Можно указать несколько доменов через запятую.
