---

id: excersise
name: Excersise
days:
- monday 
- tuesday 
- wednesday 
- thursday 
- friday
start_time: 05:30
end_time: 06:00
banner: "[[imgs/banners/695b874ffe3b6ab1f12ff09a7762284a.jpg]]"
pixel-banner-flag-color: white
content-start: 161
banner-x: 3
banner-y: 34
banner-display: cover
banner-fade: 100
banner-height: 160
---

# 🛠 Edición rápida

## Name: `INPUT[text():name]`  

## Description

```meta-bind
INPUT[textArea(class(meta-bind-full-width), class(meta-bind-high)):description]
```

## On days:

```meta-bind
INPUT[multiSelect(
option(monday) ,option(tuesday) ,option(wednesday) ,option(thursday) ,option(friday) ,option(saturday) ,option(sunday)
):days]
```

**From**: `INPUT[time:start_time]`  to `INPUT[time:end_time]`
