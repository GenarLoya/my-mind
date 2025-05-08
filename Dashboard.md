---
banner: "[[imgs/banners/dashboard.png]]"
---

## 🗂️ Habits Summary

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

## 🗂️ Tasks

```dataviewjs
const tasks = dv.pages('"Tasks"')
    .where(p => p.due)
    .sort(p => p.due, 'asc');

if (tasks.length === 0) {
    dv.paragraph("> ✅ No tasks with a due date.");
} else {
    const today = window.moment().startOf('day');

    const filtered = tasks.values.filter(p => {
        const { due, completed } = p.file.frontmatter;
        const dueDate = moment(due);

        const isOverdue = !completed && dueDate.isBefore(today);
        const isRecentlyCompleted = completed && dueDate.isSameOrAfter(today.clone().subtract(5, 'days'));

        return isOverdue || isRecentlyCompleted;
    });

    if (filtered.length === 0) {
        dv.paragraph("> 💤 No overdue or recently completed tasks.");
    } else {
        dv.list(filtered.map(p => {
            const { due, completed } = p.file.frontmatter;
            const dueDate = moment(due);
            const checked = completed ? "✅" : "☐";
            const dueStr = dueDate.format("YYYY-MM-DD");
            const overdueTag = (!completed && dueDate.isBefore(today)) ? " ⚠️ Overdue" : "";

            return `${checked} [[${p.file.folder}/${p.file.name}]] — 📅 ${dueStr}${overdueTag}`;
        }));
    }
}

```
