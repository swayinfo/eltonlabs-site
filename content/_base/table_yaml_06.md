---
{"publish":true,"created":"2025-08-02T13:56:00.279+03:00","modified":"2025-08-02T13:56:00.287+03:00","cssclasses":""}
---

## Для создания вот такого прогресс бара с развитием, нужно вставить в ежедневные заметки YAML:

![[0. Files/Pasted image 20250526143324.png]]
![[0. Files/Pasted image 20250526143440.png]]


и затем в заметке "Май 2025" вставить следующий код:

```
```dataviewjs
const pages = dv.pages('"2. Areas/Мой дневник/1-3 Daily notes"')
  .where(p => p.date && p.date.toString().includes("-05-2025"))

const totalDays = 31
const count = (key) => pages.filter(p => p[key] === true).length

const habits = [
  { name: "Разминка", key: "разминка" },
  { name: "Спортпитание", key: "спортпитание" },
  { name: "Чтение", key: "Чтениекниг" }
]

function getColor(percent) {
  if (percent >= 80) return "#4CAF50"  // зелёный
  if (percent >= 50) return "#FFC107"  // жёлтый
  return "#F44336"                     // красный
}

if (pages.length === 0) {
  dv.paragraph("❌ Нет данных за май.");
} else {
  const container = this.container

  habits.forEach(habit => {
    const current = count(habit.key)
    const percent = Math.round((current / totalDays) * 100)
    const color = getColor(percent)

    const block = document.createElement("div")
    block.style.marginBottom = "16px"

    const label = document.createElement("div")
    label.textContent = `${habit.name}: ${percent}%`
    label.style.fontWeight = "bold"
    label.style.marginBottom = "4px"

    const barContainer = document.createElement("div")
    barContainer.style.background = "#eee"
    barContainer.style.borderRadius = "6px"
    barContainer.style.height = "16px"
    barContainer.style.width = "100%"
    barContainer.style.overflow = "hidden"

    const bar = document.createElement("div")
    bar.style.background = color
    bar.style.height = "100%"
    bar.style.width = `${percent}%`
    bar.style.transition = "width 0.3s"

    barContainer.appendChild(bar)
    block.appendChild(label)
    block.appendChild(barContainer)
    container.appendChild(block)
  })
}```
```

-> const pages = dv.pages('"2. Areas/Мой дневник/1-3 Daily notes"') — заменить на свой путь, в котором лежат наши заметки с YAML
-> Последние три символа апострофа перенести на новую строку


---

### 🧠 Пояснение для тех, кто хочет глубже понимать о чем этот код:

#### 📁 1. Что нужно добавить в ежедневные заметки

![[_base/0. Files/Pasted image 20250527143157.png]]


---

#### 💻 2. Как выглядит код в заметке “Май 2025”

В заметке месяца (например, `Май 2025`) вставь следующий код:

````markdown
```dataviewjs
const pages = dv.pages('"2. Areas/Мой дневник/1-3 Daily notes"')
  .where(p => p.date && p.date.toString().includes("-05-2025"))
````

🛠 **Объяснение:**

- `pages` — мы берём все дневники из папки.
    
- Фильтруем только за май 2025 (`includes("-05-2025")`).
    
- Не забудь заменить путь на свой!
    

---

```js
const totalDays = 31
const count = (key) => pages.filter(p => p[key] === true).length
```

- `totalDays` — общее число дней в месяце.
    
- `count()` — сколько дней привычка была выполнена.
    

---

```js
const habits = [
  { name: "Разминка", key: "разминка" },
  { name: "Спортпитание", key: "спортпитание" },
  { name: "Чтение", key: "Чтениекниг" }
]
```

🔑 Здесь ты задаёшь **список привычек**, которые будешь отслеживать.

- `name` — как будет называться на экране.
    
- `key` — как поле записано в YAML.
    

---

```js
function getColor(percent) {
  if (percent >= 80) return "#4CAF50"  // зелёный
  if (percent >= 50) return "#FFC107"  // жёлтый
  return "#F44336"                     // красный
}
```

🟩 Зелёный = ты молодец  
🟨 Жёлтый = стараешься  
🟥 Красный = нужна дисциплина

---

#### 📊 Визуализация

Внутри цикла `habits.forEach(...)` создаётся:

- **текст с процентом выполнения привычки**;
    
- **контейнер с серой полоской**;
    
- **цветной прогресс-бар**, который заполняется в зависимости от %.
    

---

##### ✅ Что в итоге

Ты получаешь **панель привычек за месяц**:

- Красиво.
    
- Мотивирует.
    
- Прямо в твоей заметке — никакие внешние трекеры не нужны.
    
