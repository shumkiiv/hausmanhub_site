# Сайт hausmanhub.ru

Продуктовый сайт HausmanHub: статические страницы для GitHub Pages с custom
domain `hausmanhub.ru`. Отдельный репозиторий, без ссылок, общих ассетов и
общего DNS с другими проектами владельца.

## Состав

- `index.html` - главная: герой, возможности, скриншоты, загрузка, поддержка.
  В `<head>` есть `<link rel="redirect_uri" href="hausmanhub://auth-callback">`:
  страница может служить hosted client_id для OAuth/IndieAuth Home Assistant
  (сейчас основной client_id отдаёт Node-RED внутри дома, см.
  `docs/HACS_OPERATIONS_RUNBOOK.md`).
- `privacy.html` - политика конфиденциальности, текст из
  `docs/product/PRIVACY_POLICY.md` (синхронизировать при изменении).
- `styles.css` - стили; цвета из `components/integration/docs/design-tokens.json`
  (accent/primary `#2F6FE4`).
- `assets/` - иконка (сгенерирована, силуэт дома на фирменном синем) и
  скриншоты 1280x800 из `artifacts/` (реальные снимки панели; публикация
  согласована владельцем 2026-08-18, исключение записано в
  `components/android/AGENTS.md`).
- `CNAME` - custom domain для GitHub Pages.

## Публикация (однократно)

1. Создать публичный репозиторий `shumkiiv/hausmanhub_site` (или иной) на
   GitHub и запушить сюда ветку `main`.
2. Settings - Pages - Source: `Deploy from a branch`, ветка `main`, папка
   `/ (root)`.
3. Settings - Pages - Custom domain: `hausmanhub.ru`, включить
   `Enforce HTTPS` (сертификат выпускается GitHub автоматически).
4. DNS у регистратора (reg.ru):
   - `A` для `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`,
     `185.199.111.153`;
   - `AAAA` для `@`: `2606:50c0:8000::153`, `2606:50c0:8001::153`,
     `2606:50c0:8002::153`, `2606:50c0:8003::153`;
   - `CNAME` для `www`: `shumkiiv.github.io` (после этого www-адрес тоже
     можно привязать в Pages как альтернативный домен).

## Известная особенность сети

Из домашней сети владельца провайдер блокирует 3 из 4 адресов GitHub Pages
(работает только `185.199.110.153`). Сайт доступен извне, но из дома может
открываться через раз; обход - запись в `/etc/hosts` либо перенос DNS на
Cloudflare. Работа планшета и OAuth от сайта не зависят: client_id отдаёт
локальный Node-RED.
