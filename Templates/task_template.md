---
<%*
const moment = window.moment;
let taskName;
while (true) {
    taskName = await tp.system.prompt("📝 Nombre de la tarea (obligatorio)");
    if (taskName?.trim()) {
	    await tp.file.rename(taskName);
	    break;
    }
    await tp.system.prompt("❌ El nombre no puede estar vacío. Presiona Enter para intentar de nuevo.");
}

const taskDescription = await tp.system.prompt("🧾 Descripción de la tarea (opcional)");

let dueDate;
while (true) {
    const input = await tp.system.prompt("📅 Fecha esperada (YYYY-MM-DD)");
    const parsed = moment(input, "YYYY-MM-DD", true);
    if (parsed.isValid()) {
        dueDate = parsed.format("YYYY-MM-DD");
        break;
    } else {
        await tp.system.prompt("❌ Fecha inválida. Usa el formato YYYY-MM-DD.");
    }
}

const id = taskName.toLowerCase().replace(/[^\w\d\-]/g, "_");
-%>
id: <% id %>
name: <% taskName %>
description: <% taskDescription %>
due: <% dueDate %>
completed: false
---
# 🛠 Edición rápida

## Completed `INPUT[toggle:completed]`

## Name: `INPUT[text():name]`  

## Description

```meta-bind
INPUT[textArea(class(meta-bind-full-width), class(meta-bind-high)):description]
```

## Due

```meta-bind
INPUT[date():due]
```
