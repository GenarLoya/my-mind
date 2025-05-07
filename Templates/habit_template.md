---
name: <% await tp.system.prompt("Please enter a value", "name")%>
---
<%*
new Notice(`status: ${tp.frontmatter.name}`);
-%>