---
name: <% await tp.system.prompt("Please enter a value", "name")%>
---
```json
<% JSON.stringify(tp.frontmatter, null, 2)%>
```
