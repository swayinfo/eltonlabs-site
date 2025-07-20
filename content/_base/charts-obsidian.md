### Плагин Charts в Obsidian

>[!quote] ![[Pasted image 20250503175950.png]]

### ❓ Что такое Charts?

**Charts** — это плагин для построения графиков прямо внутри Obsidian.  

>[!example] Например: 
>Если ты ведёшь учёт веса, расходов, идей или чего угодно числового — теперь это можно **наглядно визуализировать**.

---

## 📊 Что можно строить?

👉 Варианты графиков (все работают через простой синтаксис в Markdown):

- **Bar chart (столбики)** — для категорий: идеи, расходы, проекты

``` Код для Charts:
chart
type: bar
labels: [Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, "next Week", "next Month"]
series:
  - title: Title 1
    data: [1, 2, 3, 4, 5, 6, 7, 8, 9]
  - title: Title 2
    data: [5, 4, 3, 2, 1, 0, -1, -2, -3]
```

>[!quote] ![[Pasted image 20250503180310.png]]

> [!quote] ![[Pasted image 20250503180248.png]]

---
- **Line chart (линейный)** — отличен для прогресса: спорт, вес, учёба

```Код для Charts:
chart
type: line
labels: [Monday, Tuesday, Wednesday, Thursday, Friday]
series:
  - title: Title 1
    data: [1, 2, 3, 4, 5]
  - title: Title 2
    data: [5, 4, 3, 2, 1]
  - title: Title 3
    data: [8, 2, 5, -1, 4]
```

>[!quote] ![[Pasted image 20250503180446.png]]

>[!quote] ![[Pasted image 20250503180456.png]]

---

- **Pie chart (пирог)** — показывает доли: где проводишь время

```Код для Charts:
chart
type: pie
labels: [Monday, Tuesday, Wednesday, Thursday, Friday]
series:
  - title: Title 1
    data: [1, 2, 3, 4, 5]
  - title: Title 2
    data: [5, 4, 3, 2, 1]
width: 40%
labelColors: true
```

>[!quote] ![[Pasted image 20250503180709.png]]

>[!quote] ![[Pasted image 20250503180725.png]]

- **Radar chart (радар)** — для самооценки по навыкам или сферам жизни
``` Код для Charts:
chart
type: radar
labels: [Monday, Tuesday, Wednesday, Thursday, Friday]
series:
  - title: Title 1
    data: [1, 2, 3, 4, 5]
  - title: Title 2
    data: [5, 4, 3, 2, 1]
width: 40%
```

>[!quote] ![[Pasted image 20250503180815.png]]

>[!quote] ![[Pasted image 20250503180823.png]]

>[!todo] 📘 Документация: [phibr0 Charts plugin](https://charts.phib.ro/Meta/Charts/Chart+Types/Pie+and+Donut+Chart)

---

## 🛠 Установка

1. Открыть `Настройки` → `Плагины сообщества`
2. Нажать `Обзор` → найти **Charts**
3. Установить и активировать

---

## 🧪 Пример: количество идей по направлениям

```код для charts:
chart
type: bar
labels: ["Marketplace", "EdTech", "No-code", "AI Tools"]
series:
  - title: Идеи
    data: [5, 8, 0, 10]
width: 80%
```
>[!quote] ![[Pasted image 20250503181213.png]]

>[!quote] ![[Pasted image 20250503181224.png]]

### 🔍 Объяснение:

- `type: bar` — тип графика: столбиковый
- `labels:` — подписи по оси X
- `series:` — название графика и значения
- `width:` — ширина графика (можно задать в %, px и т.п.)

---

## ⚖ Пример из жизни: трекинг веса

Ты ведёшь таблицу с весом по месяцам в заметке `Areas > Занятие спортом > Динамика веса`:

| Месяц   | Вес |
| ------- | --- |
| Январь  | 70  |
| Февраль | 65  |
| Март    | 68  |
| Апрель  | 70  |
| Май     | 71  |
Ниже добавляем `^weightTable`
Это называется ID, мы даем плагину Charts понять, что ID это таблица.

```код для charts
chart
type: line
id: weightTable
labelColumn: Месяц
valueColumn: Вес
width: 100%
tension: 0.4
beginAtZero: false
fill: false
smoothLines: true
```

>[!quote] ![[Pasted image 20250503181428.png]]

>[!quote] ![[Pasted image 20250503181441.png]]



---

## 📊 Что ещё можно:

- Статистика чтения книг по месяцам
- Расходы на подписки
- Время, уделённое разным проектам
- Личный дэшборд: графики, заметки, трекеры — всё на одной странице

---

>[!tip] 💬 Совет: не знаешь, как правильно написать код?  
> Обратись в наш чат по Obsidian, или попроси ChatGPT помочь на основе структуры твоего хранилища.

---

> [!abstract] Идем дальше?
> - 🧠 [[pomodoro-timer|Pomodoro — 25 минут работает, 5 минут отдыхаем]]
> - [[Home|⬅️ Назад на главную]]

