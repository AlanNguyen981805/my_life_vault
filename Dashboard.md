
------------------------


## ⚡ Hôm nay & quá hạn

```dataview
TASK
FROM "Projects"
WHERE !completed
GROUP BY file.link
```

---

## 📁 Tổng quan tất cả dự án

```dataviewjs
// Lấy mọi note trong thư mục "Projects" (khớp với cách block task đang chạy)
// Đổi "Projects" nếu thư mục của bạn tên khác (vd "3-Projects")
const projects = dv.pages('"Projects"').where(p => p.status != "done");

if (!projects.length) {
  dv.paragraph("_Không tìm thấy dự án trong thư mục Projects._");
} else {
  const rows = [];
  for (const p of projects) {
    const top = p.file.tasks.where(t => !t.parent);
    const done = top.where(t => t.completed).length;
    const total = top.length;
    const pct = total ? Math.round(done / total * 100) : 0;

    const h = { "on-track": "🟢", "at-risk": "🟡", "off-track": "🔴" }[p.health] ?? "⚪";

    let left = 999999, dueTxt = "—";
    if (p.due_date) {
      const d = dv.date(p.due_date);
      left = Math.ceil((d - dv.date("today")) / 86400000);
      if (left < 0)        dueTxt = "🔴 quá " + Math.abs(left) + "d";
      else if (left === 0) dueTxt = "🟡 hôm nay";
      else if (left <= 2)  dueTxt = "🟡 " + d.toFormat("dd/MM");
      else                 dueTxt = d.toFormat("dd/MM");
    }

    rows.push({ link: p.file.link, h, pct, done, total, dueTxt, left });
  }

  rows.sort((a, b) => a.left - b.left);

  dv.table(
    ["Dự án", "❤️", "Tiến độ", "Deadline"],
    rows.map(r => [r.link, r.h, `${r.pct}% (${r.done}/${r.total})`, r.dueTxt])
  );
}
```

---

## 🚧 Đang chờ / bị block

```tasks
not done
(description includes #blocked) OR (is blocked)
short mode
```