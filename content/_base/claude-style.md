---
{"publish":true,"description":"Подробное руководство по созданию персональных стилей в Claude AI: психолог, юрист, копирайтер, преподаватель. Настройка custom стилей и автоматизация через текстовые экспандеры","created":"2025-08-02T13:55:59.538+03:00","modified":"2025-08-02T13:55:59.550+03:00","cssclasses":""}
---


# Стили Claude: создаем собственных ассистентов для любых задач

![[0. Files/2. Images/claude19.jpg]]

**Стили в Claude** — это революционная функция, которая позволяет создавать персонализированных ассистентов для различных сфер деятельности. 

В отличие от ChatGPT, где стиль применяется ко всем диалогам, Claude позволяет ситуационно выбирать нужный подход к общению.

## Проблема универсальных стилей в других ИИ

### 🤖 Что не так с ChatGPT?

**Проблема ChatGPT:** В настройках можно указать только один общий стиль ответов, который применяется ко всем диалогам.

![[0. Files/2. Images/claude20.jpg]]

**Реальный пример из жизни:**

- Настроили мотивирующий стиль для работы
- Спрашиваете: "Как починить ручку двери?"
- Получаете: _"Поверь в себя! Ты обязательно справишься с этой дверной ручкой! Каждый мастер начинал с малого..."_ 🤦‍♂️

### ✅ Решение Claude: ситуационные стили

Claude позволяет **динамически выбирать стиль** в зависимости от задачи:

- **Деловая переписка** → Formal стиль
- **Обучение программированию** → Explanatory стиль
- **Быстрые вопросы** → Concise стиль
- **Психологическая поддержка** → Custom "Психолог" стиль

---
# 📋 Стандартные стили

**🎯 Normal — стандартные ответы**

- Сбалансированный подход
- Средняя длина ответов
- Универсальный тон
- _Когда использовать:_ для большинства повседневных задач

**⚡ Concise — короткие ответы, чисто по делу**

- Максимально сжатая информация
- Без лишних подробностей
- Прямые ответы на вопросы
- _Когда использовать:_ для быстрых справок и фактов

**🎓 Formal — научный подход**

- Академический стиль изложения
- Использование терминологии
- Структурированная подача
- _Когда использовать:_ для документов, исследований, презентаций

**📚 Explanatory — образовательные ответы**

- ⭐ **Самый популярный стиль!**
- Подробные объяснения с примерами
- Пошаговые инструкции
- Контекст и предыстория
- _Когда использовать:_ для изучения новых тем

> 💡 **Лайфхак:** Explanatory стиль идеально подходит для освоения новой информации — Claude не просто даст ответ, но и объяснит "почему" и "как".

---
## Создание собственных стилей

![[0. Files/2. Images/claude21.jpg]]

**Шаг 1:** Нажмите "Инструменты" → "Использовать стили"

**Шаг 2:** Выберите "Создать и редактировать стили"

**Шаг 3:** Нажмите "Создать новый стиль"

**Шаг 4:** Выберите способ создания:

- **Загрузить инструкцию** — готовый файл с описанием стиля
- **Вставить текст** — образец стиля известного автора
- **Создать с подсказками** — пошаговый мастер

### 🧠 Готовые промпты для создания стилей

#### **Психолог-консультант**

```
Название: Психолог-консультант

Инструкция: Отвечай как опытный психолог-консультант:
- Определи возможную психологическую проблему или состояние
- Предложи 2-3 конкретных пути решения
- Задай 5 уточняющих вопросов для глубокого понимания ситуации
- Используй эмпатичный и поддерживающий тон
- Избегай диагнозов, фокусируйся на практических советах
- Предлагай техники и упражнения для самопомощи

Пример ответа: "Судя по вашему описанию, это может быть связано с [состояние]. Рекомендую попробовать [техника]. Расскажите, как долго это продолжается?"
```

#### **Копирайтер-маркетолог**

```
Название: Копирайтер-маркетолог

Инструкция: Отвечай как креативный копирайтер с опытом в маркетинге:
- Создавай цепляющие заголовки и слоганы
- Используй психологические триггеры и техники продаж
- Адаптируй тон под целевую аудиторию
- Предлагай варианты для A/B тестирования
- Объясняй выбор слов и приемов
- Думай о конверсии и действии пользователя

Структура ответа:
1. Анализ задачи и аудитории
2. 3-5 вариантов текста
3. Объяснение использованных приемов
4. Рекомендации по тестированию
```

#### **Программист-ментор**

```
Название: Программист-ментор

Инструкция: Отвечай как опытный senior разработчик:
- Объясняй концепции простым языком с аналогиями
- Показывай код с подробными комментариями
- Указывай на потенциальные проблемы и best practices
- Предлагай альтернативные решения
- Задавай уточняющие вопросы о контексте задачи
- Рекомендуй ресурсы для дальнейшего изучения

Формат ответа:
1. Краткое объяснение концепции
2. Пример кода с комментариями
3. Возможные улучшения
4. Ссылки на документацию
```

#### **Бизнес-аналитик**

```
Название: Бизнес-аналитик

Инструкция: Отвечай как опытный бизнес-аналитик:
- Анализируй ситуацию с точки зрения KPI и ROI
- Предлагай метрики для измерения успеха
- Используй frameworks (SWOT, Porter's 5 Forces, etc.)
- Структурируй ответы в виде списков и таблиц
- Запрашивай дополнительные данные для анализа
- Фокусируйся на практических решениях

Структура:
1. Анализ текущей ситуации
2. Ключевые проблемы и возможности
3. Рекомендации с приоритизацией
4. Метрики для отслеживания прогресса
```

### 📝 Создание стиля по образцу

**Метод "Стиль известного автора":**

1. **Выберите автора** — блогер, писатель, эксперт
2. **Найдите 3-5 текстов** этого автора
3. **Объедините в один файл** и загрузите в Claude
4. **Промпт:** "Проанализируй стиль написания этого автора и создай инструкцию для имитации его стиля"

**Пример для стиля YouTube-блогера:**

```
Анализируй стиль этого YouTube-блогера и создай инструкцию:
- Как он структурирует контент
- Какие слова и фразы использует
- Как обращается к аудитории  
- Какой тон и настроение
- Как подает сложную информацию

Создай стиль для написания скриптов в его манере.
```

## Автоматизация стилей через текстовые экспандеры

### 🚀 Beeftext для Windows

![[0. Files/2. Images/claude22.jpg]]

**Beeftext** — бесплатная программа для автоматической замены текста.

**Настройка:**

1. Скачайте Beeftext с официального сайта
2. Создайте новую комбинацию
3. **Keyword:** `клодпсих`
4. **Replacement:** полный промпт для психолога-консультанта

**Результат:** Напишите `клодпсих` в любом месте → автоматически вставится полный промпт

### 🍎 Raycast для macOS

**Raycast** — продвинутый лаунчер с поддержкой сниппетов.

**Настройка:**

1. Установите Raycast
2. Перейдите в Extensions → Snippets
3. Создайте новый сниппет с keyword
4. Добавьте полный промпт для стиля

---
## Практические сценарии использования

### 💼 Для бизнеса

**Утром — Email менеджер:**

```
Отвечай как профессиональный email-менеджер:
- Краткие и четкие ответы
- Деловой, но дружелюбный тон
- Структурированная подача информации
- Call-to-action в каждом письме
```

**Днем — Контент-стратег:**

```
Работай как опытный контент-стратег:
- Создавай идеи для социальных сетей
- Адаптируй контент под разные платформы
- Анализируй тренды и вовлеченность
- Предлагай креативные форматы
```

### 🎓 Для обучения

**Изучение языков — Полиглот:**

```
Отвечай как преподаватель иностранных языков:
- Объясняй грамматику простыми словами
- Приводи примеры из повседневной жизни
- Исправляй ошибки с объяснениями
- Предлагай упражнения для закрепления
```

**Программирование — Code Review:**

```
Работай как senior developer на code review:
- Анализируй код на читаемость и производительность
- Предлагай улучшения с объяснениями
- Указывай на потенциальные баги
- Рекомендуй best practices
```

### 🏠 Для личной жизни

**Планирование — Life Coach:**

```
Отвечай как личный коуч по продуктивности:
- Помогай ставить и достигать цели
- Создавай реалистичные планы
- Мотивируй и поддерживай
- Анализируй препятствия и их решения
```

## Комбинирование стилей с другими функциями

### 🔍 Стиль + Расширенное мышление

**Мощная комбинация:**

- Включите "Расширенное мышление"
- Выберите Explanatory стиль
- Активируйте "Исследовательский режим"

**Результат:** Получите детальный анализ с видимой логикой рассуждений и актуальной информацией.

### 📁 Стиль + Проекты

**Создание специализированных проектов:**

1. Создайте проект для конкретной сферы
2. Настройте соответствующий стиль как default
3. Добавьте релевантные файлы и документы
4. Используйте для повторяющихся задач

## Управление стилями: best practices

### 📊 Организация стилей

**Категории стилей:**

- **Работа:** Formal, Business Email, Code Review
- **Творчество:** Copywriter, Content Creator, Storyteller
- **Обучение:** Explanatory, Mentor, Language Teacher
- **Личное:** Life Coach, Psychologist, Friend

### 🔄 Итерация и улучшение

**Процесс оптимизации стилей:**

1. **Создайте базовую версию** стиля
2. **Протестируйте** на разных задачах
3. **Соберите обратную связь** от результатов
4. **Улучшите** инструкции и примеры
5. **Добавьте специфичные** требования

**Пример улучшения:**

```
Версия 1.0: "Отвечай как психолог"
↓
Версия 2.0: "Отвечай как психолог, задавай уточняющие вопросы"
↓
Версия 3.0: "Отвечай как психолог, определи проблему, предложи решения, задай 5 вопросов"
```

### 📈 Аналитика эффективности

**Критерии оценки стилей:**

- **Соответствие задаче** — получаете ли нужный результат?
- **Консистентность** — стабильное качество ответов?
- **Время экономии** — насколько быстрее решаете задачи?
- **Качество результата** — улучшилось ли качество работы?

## Продвинутые техники

### 🎭 Мульти-персона стили

**Создание "команды экспертов":**

```
Название: Команда экспертов

Инструкция: Отвечай от лица команды из 3 специалистов:
- Технический эксперт (фокус на реализации)
- Бизнес-аналитик (фокус на прибыльности)  
- UX-дизайнер (фокус на пользователе)

Каждый дает свою точку зрения, в конце - общий вывод команды.
```

### 🔀 Адаптивные стили

**Стиль, меняющийся по контексту:**

```
Инструкция: Адаптируй стиль под тип вопроса:
- Технический вопрос → детальное объяснение с примерами
- Творческий запрос → вдохновляющий и креативный подход
- Проблема → аналитический и решение-ориентированный стиль
- Личный вопрос → эмпатичный и поддерживающий тон

Определи тип вопроса и автоматически переключись на нужный стиль.
```

## Заключение

Стили Claude открывают невероятные возможности для персонализации ИИ-ассистента под любые задачи. В отличие от ChatGPT с его универсальным подходом, Claude позволяет:

✅ **Ситуационный выбор** стиля под конкретную задачу  
✅ **Создание персональных** ассистентов для разных сфер  
✅ **Автоматизацию** через текстовые экспандеры  
✅ **Гибкую настройку** и постоянное улучшение

Комбинируя стили с другими функциями Claude (проекты, расширенное мышление, артефакты), вы получаете мощную систему для решения любых задач — от психологической поддержки до бизнес-анализа.

> 🎯 **Начните с простого:** Создайте 2-3 стиля для ваших основных задач, протестируйте их и постепенно расширяйте коллекцию.

> 📺 **Смотрите демонстрацию:** [Создание персональных ассистентов в Claude](https://youtube.com/@eltonlabs)

---

**Связанные статьи:**

- [[_base/claude-artifacts\|Артефакты Claude: игры, квесты, ассистенты]]
- [[_base/claude-extenden-thinking\|Глубокий анализ от Claude: тройной режим]]
- [[_base/claude-projects\|Проекты в Claude - для продвинутых рутинных задач]]

**Теги:** #Claude #Стили #Персонализация #Ассистенты #Автоматизация #AI