## Для создания вот такой таблицы, вам нужны установить плагин Dataview, а также включить в заметке YAML

![[base/0. Files/Pasted image 20250526141546.png]]

Код для вставки:
```
```dataviewjs
const pages = dv.pages('"3. Resourses"').where(p => p.страница && p["всего страниц"]);
const container = this.container;

// === UI: Фильтр по категориям ===
const filterWrapper = document.createElement("div");
filterWrapper.style.display = "flex";
filterWrapper.style.gap = "1rem";
filterWrapper.style.marginBottom = "1rem";

// Категории (tags)
const select = document.createElement("select");
const allOption = document.createElement("option");
allOption.textContent = "Все категории";
allOption.value = "";
select.appendChild(allOption);

const allTags = new Set();
for (let p of pages) {
  const tags = Array.isArray(p.tags) ? p.tags : [p.tags];
  tags.forEach(t => t && allTags.add(t));
}
for (let tag of Array.from(allTags).sort()) {
  const opt = document.createElement("option");
  opt.textContent = tag;
  opt.value = tag;
  select.appendChild(opt);
}
filterWrapper.appendChild(select);

// === UI: Поле поиска ===
const searchInput = document.createElement("input");
searchInput.type = "text";
searchInput.placeholder = "🔍 Поиск книги...";
searchInput.style.flex = "1";
filterWrapper.appendChild(searchInput);

// === Рендер таблицы ===
container.appendChild(filterWrapper);

function renderTable(selectedTag = "", searchTerm = "") {
  const oldTable = container.querySelector("table");
  if (oldTable) oldTable.remove();

  const table = document.createElement("table");
  table.className = "dataview table-view-table";

  const header = table.insertRow();
  ["📕 Обложка", "📘 Книга", "✍️ Автор", "📚 Категория", "📖 Прочитано", "📈 Прогресс-бар"].forEach(title => {
    const th = document.createElement("th");
    th.textContent = title;
    header.appendChild(th);
  });

  for (let p of pages) {
    const tagMatch = !selectedTag || (Array.isArray(p.tags) ? p.tags.includes(selectedTag) : p.tags === selectedTag);
    const searchMatch = !searchTerm || p.file.name.toLowerCase().includes(searchTerm.toLowerCase());

    if (!(tagMatch && searchMatch)) continue;

    const current = Number(p.страница);
    const total = Number(p["всего страниц"]);
    const percent = Math.round((current / total) * 100);
    const color = percent === 100 ? 'green' : 'orange';

    const row = table.insertRow();

    const cellCover = row.insertCell();
    cellCover.innerHTML = p.cover ? `<img src="${p.cover}" width="100" style="border-radius: 8px;">` : "—";

    const cellTitle = row.insertCell();
    const link = document.createElement("a");
    link.href = p.file.path;
    link.textContent = p.file.name;
    link.className = "internal-link";
    cellTitle.appendChild(link);

    const cellAuthor = row.insertCell();
    cellAuthor.textContent = p.Автор || "–";

    const cellTags = row.insertCell();
    cellTags.textContent = Array.isArray(p.tags) ? p.tags.join(", ") : (p.tags || "–");

    const cellProgressText = row.insertCell();
    cellProgressText.textContent = `${current} / ${total}`;

    const cellBar = row.insertCell();
    const progressBarContainer = document.createElement("div");
    progressBarContainer.style.background = "#eee";
    progressBarContainer.style.borderRadius = "6px";
    progressBarContainer.style.height = "16px";
    progressBarContainer.style.width = "100%";
    const progressBar = document.createElement("div");
    progressBar.style.background = color;
    progressBar.style.height = "100%";
    progressBar.style.borderRadius = "6px";
    progressBar.style.width = `${percent}%`;
    progressBarContainer.appendChild(progressBar);
    const percentText = document.createElement("div");
    percentText.style.fontSize = "12px";
    percentText.style.textAlign = "right";
    percentText.textContent = `${percent}%`;
    cellBar.appendChild(progressBarContainer);
    cellBar.appendChild(percentText);
  }

  container.appendChild(table);
}

// === Слушатели ===
select.onchange = () => renderTable(select.value, searchInput.value);
searchInput.oninput = () => renderTable(select.value, searchInput.value);

// Инициализация
renderTable();```
```

-> from "const pages = dv.pages('"3. Resourses"')" — заменить на свой путь, в котором лежат наши заметки с YAML
-> Последние три символа апострофа перенести на новую строку


---



### 🧠 Пояснение для тех, кто хочет глубже понимать о чем этот код:


#### 🔍 1. Загружаем книги из папки

```js
const pages = dv.pages('"3. Resourses"')
  .where(p => p.страница && p["всего страниц"]);
```

Здесь мы:

- Берём все заметки из папки `"3. Resourses"` (замени путь под себя).
    
- Фильтруем только те, где есть поля `страница` (текущая страница) и `всего страниц`.
    

📌 То есть ты отслеживаешь, сколько прочитал от каждой книги — прямо в YAML.

---

#### 🧰 2. Создаём интерфейс — фильтр и поиск

```js
const filterWrapper = document.createElement("div");
...
```

Здесь создаются **два элемента управления**:

- выпадающий список с категориями (по `tags`);
    
- поле поиска по названию файла (имя заметки = название книги).
    

📌 Всё делается вручную через `document.createElement`, чтобы элемент был встроен прямо в заметку.

---

#### 🧠 3. Собираем уникальные категории

```js
for (let p of pages) {
  const tags = Array.isArray(p.tags) ? p.tags : [p.tags];
  tags.forEach(t => t && allTags.add(t));
}
```

Мы обходим все книги и собираем **уникальные теги** (категории) в список.

---

#### 📋 4. Рисуем таблицу книг

```js
function renderTable(selectedTag = "", searchTerm = "") {
```

Функция `renderTable`:

- фильтрует книги по категории и поиску;
    
- создаёт таблицу с обложками, авторами, прогрессом;
    
- пересоздаёт таблицу при каждом новом фильтре/поиске.
    

📌 Именно эта функция делает твою таблицу **живой и обновляемой**.

---

#### 🖼️ 5. Что выводится в строке таблицы?

В каждой строке — 6 ячеек:

|Колонка|Что показывает|
|---|---|
|📕 Обложка|Картинка, если указана `cover:` в YAML|
|📘 Книга|Название книги — как ссылка на заметку|
|✍️ Автор|Поле `Автор:` из YAML|
|📚 Категория|Теги книги|
|📖 Прочитано|Формат `23 / 200`|
|📈 Прогресс|Визуальный progress bar|

---

#### 🌡️ Прогресс-бар в действии

```js
const percent = Math.round((current / total) * 100);
const color = percent === 100 ? 'green' : 'orange';
```

- Вычисляется % прочитанного;
    
- Если дочитал до конца — зелёный;
    
- Если ещё читаешь — оранжевый.
    

Визуальный индикатор прямо в Obsidian — как в привычных трекерах.

---

#### 🎮 6. Добавляем "жизнь"

```js
select.onchange = () => renderTable(select.value, searchInput.value);
searchInput.oninput = () => renderTable(select.value, searchInput.value);
```

Когда пользователь меняет категорию или вводит запрос — таблица **перерисовывается** с учётом фильтров.

---

#### 🧩 Что тебе нужно для запуска

- Папка с заметками о книгах;
    
- В каждой заметке должен быть YAML с такими полями:
    

```yaml
cover: https://link.to/cover.jpg
Автор: Имя Автора
tags: [Продуктивность, Философия]
страница: 80
всего страниц: 200
```

---

### 💥 Что ты получаешь

- **Каталог книг с фильтрами и поиском**;
    
- Красивый визуал — обложки, прогресс, категории;
    
- Работает **прямо в Obsidian**, без внешних сервисов.
