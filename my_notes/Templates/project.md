---
Заметка создана: {{date}} {{time}}
Начало проекта: {{date}} {{time}}
Статус проекта: В работе
project_goal: 
Прогресс: 0
Тэги: [project]
---

# {{title}}

## 📊 Общая информация
**Статус:** `= this.project_status`
**Дата начала:** `= this.project_start`
**Цель:** `= this.project_goal`

```dataviewjs
// Расчет длительности проекта
const start = dv.date(dv.current().project_start);
const now = dv.date('now');
let end = now;

if (dv.current().project_status === "completed") {
    end = dv.current().project_end ? dv.date(dv.current().project_end) : now;
}

const duration = DateTime.fromJSDate(end).diff(DateTime.fromJSDate(start), ['days', 'hours', 'minutes']).toObject();

// Прогресс-бар
const progress = dv.current().progress || 0;
const progressBar = "█".repeat(Math.floor(progress / 10)) + "░".repeat(10 - Math.floor(progress / 10));

// Отображение
dv.el("div", `
### ⏱️ Время работы над проектом
**${Math.floor(duration.days)} дней, ${Math.floor(duration.hours)} часов, ${Math.floor(duration.minutes)} минут**

### 📈 Прогресс проекта
${progressBar} ${progress}%

### 🎯 Регулятор прогресса
<progress value="${progress}" max="100" style="width: 100%; height: 20px;"></progress>
`);

// Блок для обновления статуса и прогресса
const status = dv.current().project_status;
const progress = dv.current().progress;

dv.el("div", `
### Быстрые команды:

**Статус проекта:** ${status}
**Прогресс:** ${progress}%

*Измените значения в свойствах выше для обновления*
`);```
