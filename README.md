# Newman Run Odyssey — MVP Prototype

Digital journal про бег и музыку. Одностраничный editorial-style прототип.

---

## Файлы проекта

```
newman-run-odyssey/
├── index.html   — вся структура страницы (HTML)
├── style.css    — все стили, цвета, типографика, адаптив
└── README.md    — этот файл
```

---

## Как запустить локально

Нужен любой локальный сервер. Самый простой вариант:

```bash
# Если есть Node.js
npx serve .

# Или Python
python3 -m http.server 8080
```

Затем открой в браузере: `http://localhost:5000` (или 8080 для Python).

> Не открывай `index.html` напрямую двойным кликом — некоторые браузеры блокируют загрузку шрифтов с `file://` протокола.

---

## Где менять тексты

Все тексты находятся в `index.html`:

| Блок | Что искать в файле |
|------|-------------------|
| Hero-заголовок | `<h1 class="hero-title">` |
| Описание журнала в hero | `<div class="hero-body">` |
| Карточки плейлистов | `<article class="playlist-card ...">` (4 карточки) |
| Примечание под плейлистами | `<div class="playlists-note">` |
| Статьи "Сегодня в журнале" | `<article class="article-card ...">` |
| Блок "О проекте" | `<section class="about">` |

---

## Где менять блок с плейлистами

В `index.html` найди секцию `<section class="playlists" id="playlists">`.

Каждая карточка — это `<article class="playlist-card card-easy">` и т.д.

Что можно менять внутри карточки:
- `<div class="card-day">` — день недели (ПН / СР / ПТ / ВС)
- `<div class="card-bpm">` — диапазон BPM
- `<h3 class="card-name">` — название плейлиста
- `<p class="card-genres">` — жанры через `·`
- `<span class="card-badge">` — название дня по-английски

Классы карточек: `card-easy`, `card-intervals`, `card-tempo`, `card-longrun`.  
Карточка INTERVALS выделена красным (`color: var(--color-accent)`) через класс `card-intervals` в `style.css`.

---

## Где менять фото

В `index.html` найди теги `<img>`:

| Место | Что искать |
|-------|-----------|
| Hero (главное фото) | `<img ... class="hero-image"` |
| Статья о забеге | `<div class="article-image-wrap">` (первая) |
| Фото-полоса (photo band) | `<div class="photo-band-image">` |

Замени значение атрибута `src` на URL нового фото или путь к локальному файлу.

---

## Где менять акцентный цвет

В `style.css` найди в начале файла:

```css
--color-accent:     #e8380d;  /* основной акцент — оранжево-красный */
--color-accent-alt: #ff5c2b;  /* более светлый вариант */
```

Измени HEX-значение на любой нужный цвет. Он автоматически применится ко всем кнопкам, тегам, бордерам карточек, ticker-полосе, статистике и т.д.

---

## Архитектура

- Чистый HTML + CSS + минимальный vanilla JS (только подсветка активного пункта меню при скролле)
- Никаких фреймворков, билд-систем, зависимостей
- Шрифты: Cabinet Grotesk (display) + Satoshi (body) через Fontshare CDN
- Фотографии загружаются из открытых источников по URL
- Адаптив: оптимизирован под desktop 1600px и mobile 390px
