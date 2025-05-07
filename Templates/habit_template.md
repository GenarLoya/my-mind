<%*
const title = tp.file.title;
let newTitle;
if (title.startsWith("Untitled")) { 
    newTitle = await tp.system.prompt("Enter note title");
    await tp.file.rename(newTitle);
}
%>
---
title: <%* tR += (newTitle || title).toLowerCase().split(" ").join("_") %>
---
