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

<%*
const dv = app.plugins.plugins.dataview.api;

// Obtener todas las notas en la carpeta "Habits"
const habits = await dv.pages('"Habits"');
const weekdays = await dv.pages('"tags/weekdays"')

if (!weekdays.values.length) {
	throw new Error("Weekdays file should be exists")
}

const weekdayTags = weekdays.file.tags.values.map(w => w.replaceAll("#", ''))

// Generar una lista de tareas (checkboxes)
habits.forEach(h => {
	console.log(h.file.frontmatter.tags)
	tR += `- [ ] [[${h.file.folder}/${h.file.name}]]\n`;
});
%>