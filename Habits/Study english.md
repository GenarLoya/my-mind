---

id: study_english
name: Study english
days:
- tuesday 
- thursday 
- null 
- null
start_time: 19:00
end_time: 21:00
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
