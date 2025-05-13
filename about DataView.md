
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

---

## 🧪 Experimental: Show All Fields Dynamically

```
table key, value
from "docs"
flatten object(entries(this), (key, value))
```

### 📁 `file` Object Date Properties in Dataview

| Property       | Description                                             | Example Output             |
| -------------- | ------------------------------------------------------- | -------------------------- |
| `file.ctime`   | **Creation date** of the file (from the OS).            | `2024-06-20T14:32:01.000Z` |
| `file.mtime`   | **Last modified date** of the file (from the OS).       | `2025-04-19T09:15:45.000Z` |
| `file.name`    | File name (no extension).                               | `MyNote`                   |
| `file.path`    | Full relative path from the vault root.                 | `Journal/2025-04-20.md`    |
| `file.folder`  | Folder containing the file.                             | `Journal`                  |
| `file.day`     | Parsed date from file name (if in `YYYY-MM-DD` format). | `2025-04-20`               |
| `file.link`    | A link to the file.                                     | `[[MyNote]]`               |
| `file.inlinks` | Files that link **to** this file.                       | List of links              |
|`file.outlinks`|Files that this file **links to**.|List of links|

---

## 🔗 Resources

- [Dataview Docs](https://blacksmithgu.github.io/obsidian-dataview/)
    
- [Dataview JS Docs](https://blacksmithgu.github.io/obsidian-dataview/api/)
    
- [Beginner’s Guide to Dataview](https://obsidian.rocks/dataview-in-obsidian-a-beginners-guide/)

---
