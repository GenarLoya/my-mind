<%*
const title = tp.file.title;
let newTitle;
if (title.startsWith("Untitled")) { 
    newTitle = await tp.system.prompt("Enter note title");
    // You can split the newTitle here and save it in another variable or variables
    await tp.file.rename(newTitle);
}
-%>
---
title: <% newTitle %>
---