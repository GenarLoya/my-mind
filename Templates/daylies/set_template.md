---
name: "{{tp_prompt:'What is the habit name?'}}"
description: "{{tp_prompt:'Brief description of the habit'}}"
tags:
  - habit
  - "{{tp_prompt:'Select days (comma-separated)', 'monday,tuesday'}}"
time: "{{tp_prompt:'At what time? (e.g. 08:00 AM)'}}"
---

# {{tp_title}}

## Habit Description
{{tp_frontmatter.description}}

## Scheduled Days
- {{tp_frontmatter.tags[1]}}

## Time
- {{tp_frontmatter.time}}
