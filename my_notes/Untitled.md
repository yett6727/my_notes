---
Заметка создана: 07.10.2025 22:42
Начало: 07.10.2025 22:42
Статус: в работе
project_goal:
Прогресс: 0
Тэги:
  - project
---

## 📈 Прогресс проекта
```dataviewjs
const progress = dv.current().Прогресс || 0;
const progressBar = "█".repeat(Math.floor(progress / 10)) + "░".repeat(10 - Math.floor(progress / 10));

dv.el("div", `
${progressBar} ${progress}%

<progress value="${progress}" max="100" style="width: 100%; height: 20px;"></progress>
`);
```

```dataviewjs
const start = dv.date(dv.current().Начало);
const now = dv.date('now');
let end = now;

if (dv.current().Статус === "завершен") {
    end = dv.current().project_end ? dv.date(dv.current().project_end) : now;
}

const duration = DateTime.fromJSDate(end).diff(DateTime.fromJSDate(start), ['days', 'hours']).toObject();

dv.el("div", `
**${Math.floor(duration.days)} дней, ${Math.floor(duration.hours)} часов**
`);
```


```dataviewjs
TABLE created AS "Создана", wordcount AS "Слов"
FROM #"{{title}}"
WHERE file.name != this.file.name
SORT created ASC
```
