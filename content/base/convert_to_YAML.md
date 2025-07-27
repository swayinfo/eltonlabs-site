###  Замена старых шаблонов на YAML + встроенные обратные ссылки

> [!warning] Сделай резервную копию 
> Перед любыми массовыми изменениями **обязательно** сделай копию своего хранилища Obsidian. Даже если всё работает идеально — ошибки случаются. Также для минимизации риска - рекомендую ручной способ.

---

## 🎯 Что мы хотим заменить?

Раньше заметки начинались вот так:

>[!quote] Шаблон для связей, который у меня сейчас:
>![[Pasted image 20250526132559.png]]

````
%%Input links:
Tags: #тег
Date: {{date}}
Output links:
```dataview
list from [[{{title}}]]
%%
````


Такой формат:
- не читается плагином Dataview
- мешает структуре заметки
- требует ручного редактирования

Мы хотим перейти на YAML:

>[!quote] Как выглядит шаблон YAML:
>![[Pasted image 20250526132739.png]]

А так выглядит YAML в виде исходного кода:
```
---
input links:
  - '[[ПСИХОЛОГИЯ]]'
tags:
  - психология
  - blog
date: 24-05-2025
---
````

А отображение обратных ссылок можно перенести в начало заметки. Каким образом? Давайте рассмотрим ниже.

---

#### 🔗Обратные ссылки — встроенная функция от Obsidian

Вместо `Output links` с кодом `[[Dataview]]`, теперь мы используем:

- **встроенные обратные ссылки** (включаются в настройках)

>[!quote] Как выглядят "Обратные ссылки":
>![[Pasted image 20250526133743.png]]
![[01.png]]

---

## 🎨 Как переместить обратные ссылки вверх, рядом с YAML, с помощью CSS

1. Открываем папку с CSS-сниппетами:
>[!quote] Папка CSS-сниппеты:
>![[Pasted image 20250526134931.png]]

2. Создаем CSS-документ (для начала создаем обычный блокнот -> "Сохранить как" -> "Все форматы" -> просто дописываем в названии файла .css -> например backlinks.css)

3. Добавь этот код в `publish.css` или `obsidian.css`:

```
.cm-sizer {
  display: flex;
  flex-direction: column;
}

.inline-title {
  order: 1;
}

.metadata-container {
  order: 2;
}

.embedded-backlinks {
  order: 3;
  position: static;
  overflow-y: auto;
  max-height: 300px;
}

.cm-contentContainer {
  order: 4;
}
```

>[!quote] Как выглядит код в блокноте (css):
>![[Pasted image 20250526135130.png]]
>


>[!quote] 👉 Теперь обратные ссылки будут сразу под YAML-блоком. Это удобно для быстрого просмотра связей.
>![[02.png]]

---

## 🔁 3 способа перехода на YAML

### 1. 🐍 Python-скрипт (для опытных)

```
# Смотри ниже — обязательно замени путь к Vault (Vault_Path) и проверь шаблон поиска
```

> [!danger] Внимание! Этот метод массово заменяет текст. Не запускай, если не уверен. Лучше проконсультируйся с ChatGPT перед запуском.

#### Вот сам код:

```
import os
import re

VAULT_PATH = r"C:\delete after\Tutorial 01"

# Гибкая регулярка: допускает необязательные пробелы, переносы и отсутствие некоторых полей
pattern = re.compile(
    r"(?:%%)?\s*\*\*Input links\*\*:\s*(.*?)"
    r"\n\s*\*\*Tags\*\*:\s*#?(.*?)"
    r"(?:\n\s*\*\*Date\*\*:\s*(.*?))?"
    r"\n\s*\*\*Output links\*\*:\s*```dataview\s*\nlist from \[\[(.*?)\]\]\s*\n```"
    r"\n___\s*(?:%%)?",
    re.DOTALL
)

def convert_file(filepath):
    with open(filepath, "r", encoding="utf-8") as f:
        content = f.read()

    if content.strip().startswith("---"):
        return False

    match = pattern.search(content)
    if not match:
        return False

    input_raw = match.group(1).strip()
    tags_raw = match.group(2).strip()
    date = match.group(3).strip() if match.group(3) else None

    # Форматирование ссылок: '[[...]]'
    input_links = re.findall(r"\[\[(.*?)\]\]", input_raw)
    input_yaml = "\n".join([f"  - '[[{link.strip()}]]'" for link in input_links])

    # Форматирование тегов
    tags = [tag.strip("# ").strip() for tag in tags_raw.split()]
    tags_yaml = "\n".join([f"  - {tag}" for tag in tags]) if tags else "  - "

    # Формируем YAML
    yaml = [
        "---",
        "input links:",
        input_yaml if input_yaml else "  - ",
        "tags:",
        tags_yaml,
    ]
    if date:
        yaml.append(f"date: {date}")
    yaml.append("---")

    # Удаляем весь старый блок и добавляем YAML
    new_content = "\n".join(yaml) + "\n\n" + content[match.end():].lstrip()

    with open(filepath, "w", encoding="utf-8") as f:
        f.write(new_content)

    print(f"✅ Обновлено: {filepath}")
    return True

def process_vault():
    print("🚀 Запускаю обработку...")
    count = 0
    for root, _, files in os.walk(VAULT_PATH):
        for file in files:
            if file.endswith(".md"):
                full_path = os.path.join(root, file)
                if convert_file(full_path):
                    count += 1
    print(f"🎉 Готово! Обновлено файлов: {count}")

if __name__ == "__main__":
    process_vault()
    
```

> [!tip] Как адаптировать под себя?
> 
> 1. Замени `VAULT_PATH` на путь к своему хранилищу
>     
> 2. Покажи этот код ChatGPT и напиши: «`Помоги адаптировать под мои шаблоны. Вот пример заметки`...»
>     

---

### 2. 🔍 Плагин Global Search and Replace

Подходит для шаблонных строк. Например:

- Найди: `%%Input links:`
- Замени на: `---\ninput links:`

Если шаблон стабилен — работает надёжно. Но смотри на отступы YAML!

---

### 3. ✍️ Ручной перенос (рекомендуется)

Лучше всё сделать вручную в 5–10 ключевых шаблонах, а потом использовать их как основу.

> [!example] Рекомендуемый подход:
> 
> - Создай шаблон YAML для разных типов заметок (книга, идея, проект)
>     
> - Удали старый блок `%%...%%`
>     
> - Включи обратные ссылки и используй CSS, чтобы они были вверху
>     

---

## 📌 Заключение

> [!success] Переход на YAML — это про порядок Ты избавляешься от ручного кода, используешь встроенные возможности Obsidian и наводишь чистоту в своей системе.

Хочешь пример адаптации под свой Vault? Напиши ChatGPT:

> «Вот как выглядел мой старый шаблон. Помоги переделать его в YAML и объясни, какие строки можно вставить вручную.»

---
> [!abstract] Идем дальше?
> - 🧠 [[YAML|Вернуться назад в YAML]]
> - [[Home|⬅️ Назад на главную]]