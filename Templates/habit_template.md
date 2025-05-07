<%*


// 1. Prompt for habit name
const habitName = await tp.system.prompt("Enter the habit name");
const titleProp = habitName.toLowerCase().replace(/\s+/g, "_");
await tp.file.rename(habitName);

-%>
---
title: <% titleProp %>
name: <% habitName %>
days:
<% selectedDays.forEach(d => `- %{d}/n`> %>
start_time: <% startTime %>
end_time: <% endTime %>
---
# <% habitName %>

Describe your habit here.
