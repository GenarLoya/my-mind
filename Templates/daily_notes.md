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
const weekdays = await dv.pages('"tags/weekdays"');

if (!weekdays.values.length) {
	throw new Error("Weekdays file should exist");
}

const weekdayTags = weekdays.file.tags.values.map(w => w.replaceAll("#", ''));

// Obtener el día actual (en minúsculas, como 'monday')
const today = window.moment().format("dddd").toLowerCase();
const todayTag = `${today}`;

let found = false;

habits.forEach(h => {
	const tags = h.file.frontmatter?.days ?? [];

	if (tags.includes(todayTag)) {
		found = true;
		tR += `- [ ] [[${h.file.folder}/${h.file.name}]]\n`;
	}
});

if (!found) {
	tR += `> 📭 No habits scheduled for today (${today.charAt(0).toUpperCase() + today.slice(1)}).\n`;
}
%>

## Tasks

