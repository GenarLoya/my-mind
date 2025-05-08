---

id: testyuekgfher
name: testyuekgfher
tags:
- #week/monday 
- #week 
- #week/tuesday 
- #week/wednesday
start_time: 09:00
end_time: 18:00
banner: "[[imgs/banners/695b874ffe3b6ab1f12ff09a7762284a.jpg]]"
pixel-banner-flag-color: white
content-start: 161
banner-x: 3
banner-y: 34
banner-display: cover
banner-fade: 100
banner-height: 160
---

# `VIEW[{distance}]`

Describe your habit here.

## Name: `INPUT[text():name]`  

## On days:

```meta-bind
INPUT[multiSelect(
- option(#week/monday) ,- option(#week) ,- option(#week/tuesday) ,- option(#week/wednesday)
):multiSelect2]
```

**From**: `INPUT[time:start_time]`  to `INPUT[time:end_time]`
