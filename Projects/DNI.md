---
fileClass: project
area: "[[Work]]"
status: in-progress
health: at-risk
priority: high
start_date: 2026-06-30
due_date: 2026-07-02
tags: [project]
---

## 📊 Trạng thái
```dataviewjs
const p = dv.current();

// Đếm task NẰM TRONG CHÍNH FILE NÀY
const tasks = p.file.tasks;
const done = tasks.where(t => t.completed).length;
const total = tasks.length;
const pct = total ? Math.round(done / total * 100) : 0;

const bar = "█".repeat(Math.round(pct/10)) + "░".repeat(10 - Math.round(pct/10));

dv.paragraph(`**Status:** ${p.status} · **Health:** ${p.health} · **Due:** ${p.due_date}`);
dv.paragraph(`**Tiến độ:** ${bar} ${pct}% (${done}/${total})`);

if (p.due_date) {
  const left = Math.ceil((dv.date(p.due_date) - dv.date("today")) / 86400000);
  dv.paragraph(`⏳ Còn **${left} ngày** tới deadline`);
}
```

## ✅ Tasks
- [ ] Họp báo cáo tiến độ 📅 2026-07-02 ⏫ 🔁 every week 
- [ ] Fix 6 bugs #doing ⏫ 🛫 2026-07-01 📅 2026-07-01