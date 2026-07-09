---
fileClass: project
area: "[[Work]]"
status: in-progress
health: at-risk
priority: high
start_date: 2026-06-30
due_date: 2026-07-02
tags:
  - project
---

- prototype: https://app.visily.ai/projects/80375a3c-8a9a-4f85-accc-ae5f0b41c330/boards/2649806
- link deploy
	- Web app: https://order-app-test.lotussolution.cloud/home
		- tk: 0912312312
		- room: 2614
	- CMS: https://order-app-cms-test.lotussolution.cloud/
		- tk: admin@mandala.local
		- mk: 12345aA@
- link api: https://docs.google.com/document/d/1V3m2pImb1asm99cfMjtF-ZoWLBBg9N1K/edit?rtpof=true&sd=true
- link SRS: https://ujbc4oj6ouc.sg.larksuite.com/docx/CJDrdUMrQoQ4SWxNu3blFoZegpN
- Tài liệu webhook gọi sang POS: https://drive.google.com/file/d/1oUXiyFyr0fpy2uoIu9F0Fqr9mw9uIuMj/view?usp=sharing
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
- [x] Rà soát hệ thống và kiểm tra thông luồng với các service khác #doing 📅 2026-07-01 ✅ 2026-07-06
- [x] Bàn giao hệ thống cho C Duyên test / ⏫ 📅 2026-07-06 ✅ 2026-07-06
	- [x] Setup data test 📅 2026-07-06 ✅ 2026-07-06
	- [x] Tích hợp thông báo telegram / ⏫ 📅 2026-07-06 ✅ 2026-07-07
	- [x] Sửa lại API web hook cho a Trường đồng nhất message lỗi / 📅 2026-07-07 ✅ 2026-07-07
	- [x] Sửa lại phần đặt lịch luồng khi đặt lịch mà lại thêm giỏ hàng là sai / ⏫ 📅 2026-07-07 ✅ 2026-07-07
	- [ ] Fix bug lỗi item ở giỏ hàng bị nhảy index khi add item không thành công /📅 2026-07-07 🔼 
	- [ ] API wehook trả cho a Trường 2 field orderNo để lưu và QR khi thanh toán /📅 2026-07-09 🔼 


```tasks
not done
path includes Order Service
```


##  ✅ Question
- [x] Hỏi lại luồng khi user tạo đơn -> duyệt -> nhỡ user hủy đơn thì sao , 🔼 📅 2026-07-06 ✅ 2026-07-06

