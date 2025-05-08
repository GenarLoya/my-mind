---

<%*
const dv = app.plugins.plugins.dataview.api;

// 1. Prompt for habit name
const habitName = await tp.system.prompt("Enter the habit name");
const titleProp = habitName.toLowerCase().replace(/\s+/g, "_");
await tp.file.rename(habitName);

// 2. Select repeat days
const weekdays = await dv.pages('"tags/weekdays"')

if (!weekdays.values.length) {
	throw new Error("Weekdays file should be exists")
}

const weekdayTags = weekdays.file.tags.values.map(w => w.replaceAll("#", ""))

const NONE = "none"
let allDays = [...weekdayTags, NONE];

let selectedDays = [];

while (true) {
    const day = await tp.system.suggester(allDays, allDays, false, "Select a day (or 'none' to finish)");


    if (day === NONE) {
	    if (!selectedDays.length) {
		    await tp.system.prompt("❌ Invalid time format. Press Enter to retry.");
		    continue;
	    }

		break;
    }
    selectedDays.push(day);
    allDays = allDays.filter(d => d !== day); // Remove selected
}

// 3. Prompt for start time
let startTime;
while (true) {
    const input = await tp.system.prompt("Enter start time (e.g., 08:00 or 8:00 am)");
    if (moment(input, ["HH:mm", "h:mm A"], true).isValid()) {
        startTime = input;
        break;
    } else {
        await tp.system.prompt("❌ Invalid time format. Press Enter to retry.");
    }
}

// 4. Prompt for end time
let endTime;
while (true) {
    const input = await tp.system.prompt("Enter end time (e.g., 18:30 or 6:30 pm)");
    if (moment(input, ["HH:mm", "h:mm A"], true).isValid()) {
        endTime = input;
        break;
    } else {
        await tp.system.prompt("❌ Invalid time format. Press Enter to retry.");
    }
}
-%>
id: <% titleProp %>
name: <% habitName %>
tags:
<% selectedDays.map(d => `- ${d}`).join(' \n') %>
start_time: <% startTime %>
end_time: <% endTime %>
banner: "[[imgs/banners/695b874ffe3b6ab1f12ff09a7762284a.jpg]]"
pixel-banner-flag-color: white
content-start: 161
banner-x: 3
banner-y: 34
banner-display: cover
banner-fade: 100
banner-height: 160
---
# <% habitName %>

Describe your habit here.
