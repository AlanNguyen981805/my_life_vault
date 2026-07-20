
# Order Service

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

### 🔗 Links
- Prototype: [Visily](https://app.visily.ai/projects/.../boards/2649806)
- API docs: [Google Doc](https://docs.google.com/document/d/1V3m2pImb1asm99cfMjtF-ZoWLBBg9N1K)
- SRS: [Larksuite](https://ujbc4oj6ouc.sg.larksuite.com/docx/CJDrdUMrQoQ4SWxNu3blFoZegpN)
- Webhook → POS: [Drive](https://drive.google.com/file/d/1oUXiyFyr0fpy2uoIu9F0Fqr9mw9uIuMj/view)

### 🔑 Môi trường TEST
| Hệ thống | URL | Tài khoản | Mật khẩu |
|----------|-----|-----------|----------|
| Web app | [link](https://order-app-test.lotussolution.cloud/home) | 0912312312 | room: 2614 |
| CMS | [link](https://order-app-cms-test.lotussolution.cloud/) | admin@mandala.local | 12345aA@ |
| POS | [link](https://sh-test.qcloud.asia/POS/#/module/03201.MMN) | admin | — |
### 🔑 Môi trường PILOT

| Hệ thống | URL                                                           | Tài khoản           | Mật khẩu   |
| -------- | ------------------------------------------------------------- | ------------------- | ---------- |
| Web app  | [link](https://order-app.lotussolution.cloud?hotelCode=MDLKB) | 0912312312          | room: 2614 |
| CMS      | [link](https://order-app-cms.lotussolution.cloud/)            | admin@mandala.local | 12345aA@   |
| POS      | [link](kb.mandal)                                             | admin               | —          |

---

## 🗂️ Kho task (fold — nơi gõ mọi task)

<!-- Gõ task ở đây. Xong tick, "Cần làm" ở trên tự lọc. - [ ] Việc cha 🔼 📅 2026-07-20 - [ ] Subtask (thụt lề) Đã xong nhiều thì fold mục này lại cho gọn. -->

- [ ]