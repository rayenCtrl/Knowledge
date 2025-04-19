
---

## 🔤 1. Data Types in Dataview

| Type        | Example                 | Notes                                   |
| ----------- | ----------------------- | --------------------------------------- |
| **String**  | `"Hello World"`         | Text, quotes needed                     |
| **Number**  | `123`, `3.14`           | Can be sorted, used in math             |
| **Date**    | `2025-04-19`            | Use `date(<string>)` to parse           |
| **Boolean** | `true`, `false`         | Often used in checkboxes                |
| **Link**    | `[[Note Name]]`         | Internal links, clickable               |
| **List**    | `[item1, item2, item3]` | Multiple values in YAML or inline       |
| **Object**  | `{key: value}`          | Key-value pairs, often from frontmatter |



## 🔍 2. Filtering Data

Use the `where` clause in Dataview to filter notes:

```
table file.name, status
from "docs"
where status = "Done"
```

More filtering examples:

```
where author = "Rayen"
where contains(tags, "obsidian")
where completed = false
where updated >= date(2024-01-01)
```


---

## 🧮 3. Data Query Types

### 📋 Table

```
table file.name, created, status
from "Projects"
where status != "Archived"
sort created desc
```

### 📌 List

```
list
from "Readings"
where contains(tags, "book")
```

### ✅ Task View

```
task
from "Daily"
where !completed
group by file.name
```

---

## 🎯 4. Creative Use Cases

### 📆 Daily Note Dashboard

```
table file.day, tasks.completed, tasks.text
from "Daily"
where file.day >= date(today) - dur(7 days)
sort file.day desc
```

### 🧠 Idea Tracker

```
list
from "Ideas"
where status != "Done"
sort created asc
```

### 📚 Book Tracker

```
table title, author, status, rating
from "Books"
where status != "Archived"
sort rating desc
```

### 🛠 Skill Tracker

```
table skill, progress, notes
from "Skills"
where progress < 100
```

---

## ✨ 5. Pro Tips

- **Inline fields** work too: `Status:: In Progress`
    
- **Aliases**: rename columns in the result with `as`
    
- **Date math**: `where due <= date(today)`
    
- **Group by**: group rows by a field
    

```
table file.name, priority
from "Tasks"
group by status
```

---

## 🧪 Experimental: Show All Fields Dynamically

```
table key, value
from "docs"
flatten object(entries(this), (key, value))
```

---

## 🔗 Resources

- [Dataview Docs](https://blacksmithgu.github.io/obsidian-dataview/)
    
- [Dataview JS Docs](https://blacksmithgu.github.io/obsidian-dataview/api/)
    
- [Beginner’s Guide to Dataview](https://obsidian.rocks/dataview-in-obsidian-a-beginners-guide/)
    

---
