<%*

const name = await tp.system.prompt("Ten du an");

const area = await tp.system.prompt("Area (Work / Personal)", "Work");

const priority = await tp.system.suggester(["high", "medium", "low"], ["high", "medium", "low"], false, "Uu tien");

const days = await tp.system.prompt("Con bao nhieu ngay toi deadline?", "7");

const due = tp.date.now("YYYY-MM-DD", parseInt(days || "7"));

await tp.file.rename(name);

-%>

---

fileClass: project

area: "[[<% area %>]]"

status: in-progress

health: on-track

priority: <% priority %>

repo: ""

start_date: <% tp.date.now("YYYY-MM-DD") %>

due_date: <% due %>

tags: [project]

---

  

# <% name %>

  

## 📊 Trạng thái

```dataviewjs

const p = dv.current();

const top = p.file.tasks.where(t => t.position.start.col === 0);

const done = top.where(t => t.completed).length;

const total = top.length;

const pct = total ? Math.round(done / total * 100) : 0;

const bar = "█".repeat(Math.round(pct/10)) + "░".repeat(10 - Math.round(pct/10));

  

dv.paragraph(`**Status:** ${p.status ?? "?"} · **Health:** ${p.health ?? "?"} · **Priority:** ${p.priority ?? "?"}`);

dv.paragraph(`**Tiến độ:** ${bar} ${pct}% (${done}/${total})`);

  

if (p.due_date) {

const left = Math.ceil((dv.date(p.due_date) - dv.date("today")) / 86400000);

const flag = left < 0 ? "🔴 QUÁ HẠN" : left <= 2 ? "🟡 GẤP" : "🟢";

dv.paragraph(`⏳ ${flag} — còn ${left} ngày (deadline ${p.due_date})`);

}

```

  

## ✅ Tasks

- [ ]

  

## 🔥 Việc chưa xong

```dataview

TASK

WHERE !completed AND file.path = this.file.path

```

  

## ✅ Đã xong

```dataview

TASK

WHERE completed AND file.path = this.file.path

SORT completion DESC

```

  

## 📝 Ghi chú / Spec

  
  

## 🔗 Liên kết

- Repo: `= this.repo`

- Area: `= this.area`