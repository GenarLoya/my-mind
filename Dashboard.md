---
banner: "[[imgs/banners/dashboard.png]]"
pixel-banner-flag-color: white
---
```dataviewjs
const today = window.moment().format("YYYY-MM-DD");
const pages = dv.pages('"Personal Journal"')
    .where(p => p.file.name === today);

if (pages.length === 0) {
    dv.paragraph(`No entry found for **${today}**.`);
} else {
    const page = pages[0];

    dv.header(3, `📝 Journal Entry for ${today}`);
    dv.paragraph(`→ [[${page.file.path}]]`);

    const allTasks = page.file.tasks || [];
    const pending = allTasks.filter(t => !t.completed);
    const completed = allTasks.filter(t => t.completed);

    if (allTasks.length === 0) {
        dv.paragraph("📭 No tasks found.");
    } else {
        dv.header(4, "🗂️ Tasks Summary");

        // Creamos tabla con dos columnas: pendientes y completadas
        const maxLength = Math.max(pending.length, completed.length);

        const tableRows = Array.from({ length: maxLength }, (_, i) => [
            pending[i]?.text || "",
            completed[i]?.text || ""
        ]);

        dv.table(["🕒 Pending", "✅ Completed"], tableRows);
    }
}

```


## Calendar

```dataviewjs
await dv.view("tasksCalendar", {pages: "", view: "month", firstDayOfWeek: "1", options: "style1"})
```

