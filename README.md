# aferia.pt — landing

Статичний сайт: HTML + CSS + мінімум JS. Хостинг — GitHub Pages (`CNAME` → `aferia.pt`).

## Структура

```
index.html                       головна
concursos/casal-de-cotao/        сторінка тендеру (noindex) — шаблон для наступних
privacidade/                     політика приватності (RGPD)
assets/styles.css                усі стилі (світла + темна тема)
assets/main.js                   мобільне меню, тінь шапки
assets/favicon.svg               favicon
assets/og.png                    Open Graph 1200×630
assets/apple-touch-icon.png      180×180
404.html, CNAME, robots.txt, sitemap.xml
```

## Контакти

Контакти підставлені прямо в HTML (без JS): `stanislav@aferia.pt` (WhatsApp поки не використовується). Змінити — пошуком по всіх `*.html`.

## Нова сторінка тендеру

1. Скопіювати `concursos/casal-de-cotao/` → `concursos/<slug>/`.
2. Оновити `<title>`, `og:url`, H1, блок `<dl class="meta">`, плашку «Prazo para erros e omissões» (поки строк відкритий — дата; після — «terminou a DD/MM/AAAA»), рядки таблиці, CTA (для відкритого строку — «Pedir o relatório completo» з `subject=Relatório <ref>`), `subject=` у `mailto:` і текст у `wa.me`.
3. `noindex` лишити, доки сторінки тендерів тестові. `robots.txt` уже закриває `/concursos/`.

## Деплой

Окремий репозиторій → Settings → Pages → Deploy from branch (`main`, `/`). Файл `CNAME` вже в корені; у DNS `aferia.pt` → A-записи GitHub Pages (185.199.108–111.153) + `www` CNAME на `<user>.github.io`.

## Варіанти дизайну

Поточний корінь — варіант «v4» (Inter, біле/сіре, звіт як інтерфейс продукту). Інші варіанти лежать поза деплой-текою, у `D:\aferia\_variants\`:
- `v1-azul/` — перший варіант (темно-синій + жовтий, сітка креслення, темна тема).
