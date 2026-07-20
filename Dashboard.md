
## ⚡ Hôm nay & quá hạn

```tasks
not done
(due on or before today)
sort by priority
group by filename
hide task count
short mode
```

---

## ⭐ Ưu tiên cao (chưa có hạn cụ thể)

```tasks
not done
priority is above medium
no due date
group by filename
short mode
```

---

## 🔜 7 ngày tới

```tasks
not done
due after today
due before in 8 days
sort by due
group by filename
short mode
```

---

## 📁 Tổng quan tất cả dự án

```dataviewjs
const projects = dv.pages('#project').where(p => p.status != "done");

if (!projects.length) {
  dv.paragraph("_Chưa có dự án nào (thiếu tag #project trong frontmatter)._");
} else {
  // sắp theo độ gấp deadline
  const rows = [];
  for (const p of projects) {
    const top = p.file.tasks.where(t => !t.parent);
    const done = top.where(t => t.completed).length;
    const total = top.length;
    const pct = total ? Math.round(done/total*100) : 0;

    const h = { "on-track":"🟢", "at-risk":"🟡", "off-track":"🔴" }[p.health] ?? "⚪";
    let left = 9999, dueTxt = "—";
    if (p.due_date) {
      const d = dv.date(p.due_date);
      left = Math.ceil((d - dv.date("today")) / 86400000);
      dueTxt = d.toFormat("dd/MM");
      if (left < 0) dueTxt = "🔴 quá " + Math.abs(left) + "d";
      else if (left <= 2) dueTxt = "🟡 " + dueTxt;
    }
    rows.push({ link: p.file.link, h, pct, done, total, dueTxt, left, status: p.status });
  }
  rows.sort((a,b) => a.left - b.left);
  dv.table(["Dự án", "Health", "Tiến độ", "Deadline"],
    rows.map(r => [r.link, r.h, `${r.pct}% (${r.done}/${r.total})`, r.dueTxt]));
}
```

---

## 🚧 Đang chờ / bị block

```tasks
not done
(description includes #blocked) OR (is blocked)
short mode
```