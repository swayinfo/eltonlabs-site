---
{"publish":true,"created":"2025-08-02T13:56:00.269+03:00","modified":"2025-08-02T13:56:00.279+03:00","cssclasses":""}
---

## Для создания вот такой таблицы, вам нужны установить плагин Dataview, а также включить в заметке YAML


>[!quote] Как выглядит простая таблица, которая берет информацию из YAML:
>![[0. Files/Pasted image 20250526142548.png]]

```
```dataviewjs
const container = this.container;

const allPages = dv.pages('"2. Areas/Сериалы и фильмы/7. Сериалы"')
    .where(p => p.Жанр && p.Рейтинг)
    .sort(p => -Number(p.Рейтинг));

// --- UI блок: Фильтр + Поиск ---
const controls = document.createElement("div");
controls.style.display = "flex";
controls.style.gap = "1rem";
controls.style.marginBottom = "1rem";

// Фильтр по жанрам
const genres = [...new Set(allPages.flatMap(p => Array.isArray(p.Жанр) ? p.Жанр : [p.Жанр]))];
const genreSelect = document.createElement("select");

const allOption = document.createElement("option");
allOption.value = "all";
allOption.textContent = "Все жанры";
genreSelect.appendChild(allOption);

for (let genre of genres.sort()) {
  const option = document.createElement("option");
  option.value = genre;
  option.textContent = genre;
  genreSelect.appendChild(option);
}
controls.appendChild(genreSelect);

// Поле поиска
const searchInput = document.createElement("input");
searchInput.type = "text";
searchInput.placeholder = "🔍 Поиск по названию...";
searchInput.style.flex = "1";
controls.appendChild(searchInput);

container.appendChild(controls);

// --- Таблица ---
const table = document.createElement("table");
table.className = "dataview table-view-table";

const header = table.insertRow();
["🎬 Обложка", "🎞 Название", "🎭 Жанр", "⭐ Рейтинг", "🧠 Инсайт"].forEach(text => {
  const th = document.createElement("th");
  th.textContent = text;
  header.appendChild(th);
});

function renderTable(filterGenre = "all", searchTerm = "") {
  table.querySelectorAll("tr:not(:first-child)").forEach(row => row.remove());

  const filteredPages = allPages.filter(p => {
    const genreMatch = filterGenre === "all" || (Array.isArray(p.Жанр) ? p.Жанр.includes(filterGenre) : p.Жанр === filterGenre);
    const searchMatch = !searchTerm || p.file.name.toLowerCase().includes(searchTerm.toLowerCase());
    return genreMatch && searchMatch;
  });

  for (let p of filteredPages) {
    const row = table.insertRow();

    const cellCover = row.insertCell();
    cellCover.innerHTML = p.Постер
      ? `<img src="${p.Постер}" width="100" style="border-radius: 8px;">`
      : "—";

    const cellTitle = row.insertCell();
    const link = document.createElement("a");
    link.href = p.file.path;
    link.textContent = p.file.name;
    link.className = "internal-link";
    cellTitle.appendChild(link);

    const cellGenre = row.insertCell();
    cellGenre.textContent = Array.isArray(p.Жанр) ? p.Жанр.join(", ") : p.Жанр;

    const cellRating = row.insertCell();
    cellRating.textContent = p.Рейтинг + "/10";

    const cellInsight = row.insertCell();
    cellInsight.textContent = p.Инсайт || "–";
  }
}

// --- Слушатели ---
genreSelect.onchange = () => renderTable(genreSelect.value, searchInput.value);
searchInput.oninput = () => renderTable(genreSelect.value, searchInput.value);

// Первый рендер
renderTable();
container.appendChild(table);```
```

-> const allPages = dv.pages('"2. Areas/Сериалы и фильмы/7. Сериалы"') — заменить на свой путь, в котором лежат наши заметки с YAML
-> Последние три символа апострофа перенести на новую строку



---



### 🧠 Пояснение для тех, кто хочет глубже понимать о чем этот код:


#### 📁 1. Загружаем заметки из нужной папки

```js
const allPages = dv.pages('"2. Areas/Сериалы и фильмы/7. Сериалы"')
    .where(p => p.Жанр && p.Рейтинг)
    .sort(p => -Number(p.Рейтинг));
```

- Здесь загружаются все заметки из папки **“Сериалы”**.
    
- Отбираются только те, где есть `Жанр` и `Рейтинг`.
    
- Сортировка по убыванию рейтинга — сверху самые топовые.
    

📌 **Замените путь на свою папку**, если структура у вас другая.

---

#### 🎛️ 2. Интерфейс: фильтр по жанру + поиск

```js
const genres = [...new Set(allPages.flatMap(...))];
```

- Собираются **все уникальные жанры** (например: Драма, Комедия, Аниме).
    
- Создаётся выпадающий список — можно отфильтровать только “Фантастику” или только “Аниме”.
    

```js
searchInput.placeholder = "🔍 Поиск по названию...";
```

- Поле поиска фильтрует по имени заметки (обычно это и есть название сериала).
    
- Работает в реальном времени — удобно!
    

---

#### 📋 3. Таблица: как выглядит каждая строка

```js
["🎬 Обложка", "🎞 Название", "🎭 Жанр", "⭐ Рейтинг", "🧠 Инсайт"]
```

Каждая строка — это один сериал, где отображается:

|Колонка|Что показывает|
|---|---|
|🎬 Обложка|Картинка из поля `Постер` (если есть)|
|🎞 Название|Название сериала, как ссылка на заметку|
|🎭 Жанр|Один или несколько жанров|
|⭐ Рейтинг|Оценка по 10-балльной шкале (`Рейтинг`)|
|🧠 Инсайт|Твоя мысль, вывод или цитата из сериала|

---

#### 🧠 4. Фильтрация и рендеринг

```js
function renderTable(filterGenre = "all", searchTerm = "") { ... }
```

- Удаляет старые строки таблицы и перерисовывает только те, что подходят под выбранный жанр или введённый текст.
    
- Это делает таблицу **живой**: реагирует на действия пользователя.
    

---

#### 🔁 5. Слушатели событий

```js
genreSelect.onchange = () => renderTable(...)
searchInput.oninput = () => renderTable(...)
```

- При смене жанра или вводе в поиск — таблица обновляется.
    
- Всё происходит **вживую**, без перезагрузки.
    

---

#### ✅ Что тебе нужно в YAML

Чтобы этот код работал, убедись, что в заметках-сериалах указаны эти поля:

```yaml
Постер: https://link-to-image.jpg
Жанр: [Фантастика, Драма]
Рейтинг: 8.7
Инсайт: Вдохновляющий взгляд на технологии будущего.
```

---

#### 🔥 Результат

Ты получаешь крутой каталог:

- всё красиво оформлено;
    
- можно фильтровать по настроению (жанр);
    
- можно быстро находить и пересматривать;
    
- можно делиться с друзьями или подписчиками.
    

---
