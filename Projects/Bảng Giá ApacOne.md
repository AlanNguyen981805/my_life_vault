

## 📊 Trạng thái

```dataviewjs
const p = dv.current();
const top = p.file.tasks.where(t => !t.parent);
const done = top.where(t => t.completed).length;
const total = top.length;
const pct = total ? Math.round(done / total * 100) : 0;
const bar = "█".repeat(Math.round(pct/10)) + "░".repeat(10 - Math.round(pct/10));

dv.paragraph(`**Tiến độ:** ${bar} ${pct}% (${done}/${total})`);

if (p.due_date) {
  const d = dv.date(p.due_date);
  const left = Math.ceil((d - dv.date("today")) / 86400000);
  let flag, txt;
  if (left < 0)        { flag = "🔴 QUÁ HẠN"; txt = `quá ${Math.abs(left)} ngày`; }
  else if (left === 0) { flag = "🟡 HÔM NAY"; txt = "hết hạn hôm nay"; }
  else if (left <= 2)  { flag = "🟡 GẤP";     txt = `còn ${left} ngày`; }
  else                 { flag = "🟢";         txt = `còn ${left} ngày`; }
  dv.paragraph(`⏳ ${flag} — ${txt} (deadline ${d.toFormat("dd/MM/yyyy")})`);
}
```

---

## 🔥 Cần làm

```dataview
TASK
WHERE !completed AND file.path = this.file.path
```

---

## 📋 Tài liệu

- Repo:
- Deploy / API / Prototype:
- link tham khảo: https://ptgkhi.netlify.app/

---

## 🗂️ Kho task (fold — nơi gõ mọi task)

<!-- Gõ task ở đây. Xong tick, "Cần làm" ở trên tự lọc. - [ ] Việc cha 🔼 📅 2026-07-20 - [ ] Subtask (thụt lề) Đã xong nhiều thì fold mục này lại cho gọn. -->

- [ ]