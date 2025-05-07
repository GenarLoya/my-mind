<%*
const moment = app.plugins.plugins["templater-obsidian"].moment;

// 1. Prompt for habit name
const habitName = await tp.system.prompt("Enter the habit name");
const titleProp = habitName.toLowerCase().replace(/\s+/g, "_");
await tp.file.rename(habitName);

// 2. Select repeat days
let allDays = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday", "none"];
let selectedDays = [];

while (true) {
    const day = await tp.system.suggester(allDays, allDays, false, "Select a day (or 'none' to finish)");
    if (day === "none") break;
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
---
title: <%= titleProp %>
name: <%= habitName %>
days:
<% selectedDays.forEach(d => { %>  - <%= d %>
<% }) %>
start_time: <%= startTime %>
end_time: <%= endTime %>
---
# <%= habitName %>

Describe your habit here.
