---
Дата: {{date}} {{time}}
Тэги: [daily, {{date: YYYY}}, {{date: MMMM}}]
Проект(-ы): 
Cлов: ${dv.current().file.words}
Настроение: 
---

## 📊 Прогресс написания
```dataviewjs
const words = dv.current().file.words || 0;
const goal = dv.current().word_goal || 500;
const percentage = Math.min(Math.round((words / goal) * 100), 100);
const progressBar = "█".repeat(Math.floor(percentage / 10)) + "░".repeat(10 - Math.floor(percentage / 10));

dv.el("div", `
**Цель:** ${goal} слов
**Написано:** ${words} слов
**Прогресс:** ${percentage}%

${progressBar} ${percentage}%

${words >= goal ? "🎉 Цель достигнута!" : `Осталось: ${goal - words} слов`}
`);