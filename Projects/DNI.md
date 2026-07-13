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
- [x] Họp báo cáo tiến độ ⏫ 🔁 every week 📅 2026-07-02 ✅ 2026-07-10
- [ ] Lỗi: fill thông tin VN title/ EN title sau đó fill các thông tin khác => Save => Mất dữ liệu VN title/ EN title 📅 2026-07-13 🔼 
- [ ] Lỗi:Doc-out gắn với case, PIC check lỗi => Cancel => Doc-out đó vẫn hiển thị trong case mà không bị xóa 📅 2026-07-13 ⏫ 
- [ ] Hỏi Hiếu phần đổi PIC trong case đang thay đổi luôn trong inquiry, bug dòng 221 📅 2026-07-14 /⏫  