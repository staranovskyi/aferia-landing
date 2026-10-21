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

## Плейсхолдери

Усі плейсхолдери — літеральні `{{...}}` у HTML, без JS-підстановки (щоб `mailto:`/`wa.me` працювали без скриптів і щоб текст був у вихідному коді для SEO).

| Плейсхолдер | Де | Значення |
|---|---|---|
| `{{EMAIL}}` | усі сторінки | `stanislav@aferia.pt` |
| `{{WHATSAPP}}` | index, concursos | номер у форматі `351XXXXXXXXX` (без `+`) |
| `{{NOME}}` | privacidade | ім'я відповідального за обробку даних |
| `{{EXPERIENCIA}}` | index → «Quem somos» | 1–2 речення з реальними фактами (або видалити `<p>`) |
| `{{PRAZO_EO}}` | concursos/casal-de-cotao | дата з Programa do Concurso |

Замінити все за раз (PowerShell, з папки `landing`):

```powershell
Get-ChildItem -Recurse -Include *.html | ForEach-Object {
  (Get-Content $_.FullName -Raw) `
    -replace '\{\{EMAIL\}\}', 'stanislav@aferia.pt' `
    -replace '\{\{WHATSAPP\}\}', '351XXXXXXXXX' `
    -replace '\{\{NOME\}\}', 'Nome Apelido' `
    -replace '\{\{EXPERIENCIA\}\}', 'Texto real.' `
    -replace '\{\{PRAZO_EO\}\}', 'DD/MM/2026' |
  Set-Content $_.FullName -NoNewline -Encoding utf8
}
```

Перевірити, що нічого не лишилось:

```powershell
Get-ChildItem -Recurse -Include *.html | Select-String '\{\{'
```

## Нова сторінка тендеру

1. Скопіювати `concursos/casal-de-cotao/` → `concursos/<slug>/`.
2. Оновити `<title>`, `og:url`, H1, блок `<dl class="meta">`, `{{PRAZO_EO}}`, рядки таблиці, `subject=` у `mailto:` і текст у `wa.me`.
3. `noindex` лишити, доки сторінки тендерів тестові. `robots.txt` уже закриває `/concursos/`.

## Деплой

Окремий репозиторій → Settings → Pages → Deploy from branch (`main`, `/`). Файл `CNAME` вже в корені; у DNS `aferia.pt` → A-записи GitHub Pages (185.199.108–111.153) + `www` CNAME на `<user>.github.io`.

## Варіанти дизайну

Поточний корінь — варіант «v4» (Inter, біле/сіре, звіт як інтерфейс продукту). Інші варіанти лежать поза деплой-текою, у `D:\aferia\_variants\`:
- `v1-azul/` — перший варіант (темно-синій + жовтий, сітка креслення, темна тема).
