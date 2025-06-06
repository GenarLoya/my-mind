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
const now = window.moment();
const today = now.format("dddd").toLowerCase();
const todayTag = `${today}`;

let todaysHabits = [];

habits.forEach(h => {
	const tags = h.file.frontmatter?.days ?? [];
	if (tags.includes(todayTag)) {
		const startStr = h.file.frontmatter?.start_time ?? "00:00";
		const endStr = h.file.frontmatter?.end_time ?? "23:59";

		const start = window.moment(startStr, "HH:mm");
		const end = window.moment(endStr, "HH:mm");

		todaysHabits.push({
			name: h.file.name,
			path: `${h.file.folder}/${h.file.name}`,
			start: startStr,
			end: endStr
		});
	}
});


if (!todaysHabits.length) {
	tR += `> 📭 No habits scheduled for today (${today.charAt(0).toUpperCase() + today.slice(1)}).\n`;
} else {
	todaysHabits.sort((a, b) => a.start.localeCompare(b.start));
	todaysHabits.forEach(h => {
		const timeStr = `⏰ **${h.start} – ${h.end}**`;
		const line = `- [ ] ${timeStr} [[${h.path}]]\n`;
		tR += line
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
        const isToday = !completed && dueDate.isSame(today, 'day');
        const isUpcoming = !completed && dueDate.isAfter(today);
        const isRecentlyCompleted = completed && dueDate.isSameOrAfter(today.clone().subtract(5, 'days'));
        return isOverdue || isToday || isUpcoming || isRecentlyCompleted;
    });

    if (filtered.length === 0) {
        dv.paragraph("> 💤 No overdue, upcoming or recently completed tasks.");
    } else {
        dv.list(filtered.map(p => {
            const { due, completed } = p.file.frontmatter;
            const dueDate = moment(due);
            const checked = completed ? "✅" : "☐";
            const dueStr = dueDate.format("YYYY-MM-DD");

            let tag = "";
            if (!completed && dueDate.isBefore(today)) tag = " ⚠️ Overdue";
            else if (!completed && dueDate.isSame(today, 'day')) tag = " 📌 Due Today";
            else if (!completed && dueDate.isAfter(today)) tag = " ⏳ Upcoming";
            else if (completed && dueDate.isSameOrAfter(today.clone().subtract(5, 'days'))) tag = " ✅ Recently Completed";

            return `${checked} [[${p.file.folder}/${p.file.name}]] — 📅 ${dueStr}${tag}`;
        }));
    }
}

```
