---
cssclasses:
  - daily
banner: "[[imgs/banners/695b874ffe3b6ab1f12ff09a7762284a.jpg]]"
pixel-banner-flag-color: white
content-start: 161
banner-x: 3
banner-y: 34
banner-display: cover
banner-fade: 100
banner-height: 160
---
# Daily Note

## Habits

<%*
const dv = app.plugins.plugins.dataview.api;

// Obtener todas las notas en la carpeta "Habits"
const habits = await dv.pages('"Habits"');
const weekdays = await dv.pages('"Tags/weekdays"');

if (!weekdays.values.length) {
	throw new Error("Weekdays file should exist");
}

const weekdayTags = weekdays.file.tags.values.map(w => w.replaceAll("#", ''));

// Obtener el día actual (en minúsculas, como 'monday')
const today = window.moment().format("dddd").toLowerCase();
const todayTag = `${today}`;

let found = false;

let todaysHabits = [];

habits.forEach(h => {
	const tags = h.file.frontmatter?.days ?? [];
	if (tags.includes(todayTag)) {
		const start = h.file.frontmatter?.start_time ?? "00:00";
		const end = h.file.frontmatter?.end_time ?? "23:59";
		todaysHabits.push({
			name: h.file.name,
			path: `${h.file.folder}/${h.file.name}`,
			start,
			end
		});
	}
});


if (!todaysHabits.length) {
	tR += `> 📭 No habits scheduled for today (${today.charAt(0).toUpperCase() + today.slice(1)}).\n`;
} else {
	todaysHabits.sort((a, b) => a.start.localeCompare(b.start));
	todaysHabits.forEach(h => {
		tR += `- [ ] ⏰ **${h.start} – ${h.end}** [[${h.path}]]\n`;
	});
}
%>

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
