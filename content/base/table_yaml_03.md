---
{"publish":true,"created":"2025-07-27T18:06:10.873+03:00","modified":"2025-08-02T13:24:03.197+03:00","cssclasses":""}
---

## Для создания вот такой таблицы, вам нужны установить плагин Dataview, а также включить в заметке YAML


>[!quote] Как выглядит простая таблица, которая берет информацию из YAML:
![[0. Files/Pasted image 20250526141442.png]]


Код для вставки:
```
```dataviewjs
const pages = dv.pages('"2. Areas/Занятие спортом/Динамика веса"')
  .where(p => p.Вес && p.date)
  .sort(p => p.date);

const labels = pages.map(p => new Date(p.date).toLocaleDateString()).array();
const values = pages.map(p => p.Вес).array();
const goal = 80;
const goals = labels.map(() => goal); // Целевая линия

const chartData = {
  type: 'line',
  data: {
    labels: labels,
    datasets: [
      {
        label: "Вес (кг)",
        data: values,
        borderColor: "blue",
        fill: false,
        tension: 0.3
      },
      {
        label: "Цель (80 кг)",
        data: goals,
        borderColor: "green",
        borderDash: [5, 5],
        pointRadius: 0,
        fill: false
      }
    ]
  },
  options: {
    responsive: true,
    plugins: {
      title: {
        display: true,
        text: "📈 Рост веса к цели"
      },
      legend: {
        position: "bottom"
      }
    },
    scales: {
      y: {
        title: {
          display: true,
          text: "Вес (кг)"
        },
        suggestedMin: 65,
        suggestedMax: 85
      },
      x: {
        title: {
          display: true,
          text: "Дата"
        }
      }
    }
  }
};

window.renderChart(chartData, this.container);```
```


-> const pages = dv.pages('"2. Areas/Занятие спортом/Динамика веса"') — заменить на свой путь, в котором лежат наши заметки с YAML
-> Последние три символа апострофа перенести на новую строку

---



### 🧠 Пояснение для тех, кто хочет глубже понимать о чем этот код:


🔹 **Что делает код:**

- Ищет все заметки из нужной папки;
    
- Фильтрует только те, где есть `Вес` и `date`;
    
- Сортирует по дате — чтобы точки шли по порядку.
    

📌 _💡 Замените путь на свой, если у вас другая папка._

---

```js
const labels = pages.map(p => new Date(p.date).toLocaleDateString()).array();
const values = pages.map(p => p.Вес).array();
```

🔹 **Что делает:**

- `labels` — это даты, по которым строим график.
    
- `values` — сами значения веса.
    

---

```js
const goal = 80;
const goals = labels.map(() => goal); // Целевая линия
```

🔹 **Что делает:**

- Мы задаём цель — например, **80 кг**.
    
- Создаём вторую линию на графике — она будет прямой, чтобы видеть, **насколько ты близко к цели**.
    

---

### 🧱 Настройка самого графика

```js
const chartData = {
  type: 'line',
  data: {
    labels: labels,
    datasets: [
      {
        label: "Вес (кг)",
        data: values,
        borderColor: "blue",
        fill: false,
        tension: 0.3
      },
      {
        label: "Цель (80 кг)",
        data: goals,
        borderColor: "green",
        borderDash: [5, 5],
        pointRadius: 0,
        fill: false
      }
    ]
  },
```

🔹 **Что делает:**

- Строит две линии:
    
    - синяя линия — твой реальный прогресс;
        
    - зелёная пунктирная — целевой вес.
        
- `tension: 0.3` — сглаживает линии (выглядит эстетично).
    
- `borderDash` — пунктир для цели, чтобы визуально отличать.
    

---

### ⚙️ Настройка внешнего вида

```js
  options: {
    responsive: true,
    plugins: {
      title: {
        display: true,
        text: "📈 Рост веса к цели"
      },
      legend: {
        position: "bottom"
      }
    },
    scales: {
      y: {
        title: {
          display: true,
          text: "Вес (кг)"
        },
        suggestedMin: 65,
        suggestedMax: 85
      },
      x: {
        title: {
          display: true,
          text: "Дата"
        }
      }
    }
  }
};
```

🔹 **Что делает:**

- Добавляет заголовок.
    
- Помещает легенду внизу.
    
- Ограничивает ось Y (от 65 до 85 кг) — чтобы график не был слишком "плоским".
    
- Подписывает оси.
    

---

```js
window.renderChart(chartData, this.container);
```

🔹 Это команда, которая **вставляет готовый график прямо в заметку Obsidian**.


    
