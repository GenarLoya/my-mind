<%*
const title = tp.file.title;
if (title.startsWith("Untitled")) { 
    const newTitle = await tp.system.prompt("Enter note title");
    // You can split the newTitle here and save it in another variable or variables
    tp.file.rename(newTitle);
}
-%>
---
title: <% newTitle %>
---