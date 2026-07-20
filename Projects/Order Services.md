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
------------------------------------------------------------------------
## TÀI LIỆU

- prototype: https://app.visily.ai/projects/80375a3c-8a9a-4f85-accc-ae5f0b41c330/boards/2649806
- link deploy
	- môi trường test
		- Web app: https://order-app-test.lotussolution.cloud/home
			- tk: 0912312312
			- room: 2614
		- CMS: https://order-app-cms-test.lotussolution.cloud/
			- tk: admin@mandala.local
			- mk: 12345aA@
		* POS TEST: https://sh-test.qcloud.asia/POS/#/module/03201.MMN
			* tk: admin
			* mk: 

- link api: https://docs.google.com/document/d/1V3m2pImb1asm99cfMjtF-ZoWLBBg9N1K/edit?rtpof=true&sd=true
- link SRS: https://ujbc4oj6ouc.sg.larksuite.com/docx/CJDrdUMrQoQ4SWxNu3blFoZegpN
- Tài liệu webhook gọi sang POS: https://drive.google.com/file/d/1oUXiyFyr0fpy2uoIu9F0Fqr9mw9uIuMj/view?usp=sharing
- Check log server:

------------------------------------------------------------------------
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
------------------------------------------------------------------------

```dataviewjs
// ============================================================
//  GANTT TIMELINE - tự sinh từ task trong file này
//  Task cần: 🛫 ngày bắt đầu  +  📅 deadline
//  VD:  - [ ] Việc A 🔼 🛫 2026-07-10 📅 2026-07-14
//  Task thiếu ngày sẽ bị bỏ qua.
// ============================================================
const p = dv.current();

// Lấy task cha có đủ start + due
const tasks = p.file.tasks.where(t => !t.parent && t.start && t.due);

if (!tasks.length) {
  dv.paragraph("_Chưa có task nào đủ 🛫 (start) và 📅 (due) để vẽ timeline._");
} else {
  let m = "gantt\n";
  m += "  dateFormat YYYY-MM-DD\n";
  m += "  axisFormat %d/%m\n";
  m += "  todayMarker on\n";
  m += "  section Tasks\n";

  for (const t of tasks) {
    const s = dv.date(t.start).toFormat("yyyy-MM-dd");
    const e = dv.date(t.due).toFormat("yyyy-MM-dd");

    // Làm sạch tên task: cắt phần emoji/ngày, bỏ ký tự gây lỗi mermaid
    let label = t.text
      .replace(/[🛫📅✅⏳⏫🔼🔽🔺⏬]/g, "")      // bỏ emoji ưu tiên/ngày
      .replace(/\d{4}-\d{2}-\d{2}/g, "")          // bỏ chuỗi ngày
      .replace(/#[^\s]+/g, "")                    // bỏ tag
      .replace(/[:;,#\[\]]/g, "")                 // bỏ ký tự làm hỏng cú pháp
      .trim()
      .slice(0, 35);                              // giới hạn độ dài
    if (!label) label = "task";

    const state = t.completed ? "done, " : "active, ";
    m += `  ${label} :${state}${s}, ${e}\n`;
  }

  dv.paragraph("```mermaid\n" + m + "```");
}
```

## 🔥 Chưa xong

```tasks
not done
path includes Order Service
```
------------------------------------------------------------------------

##  ✅ Question
- [x] Hỏi lại luồng khi user tạo đơn -> duyệt -> nhỡ user hủy đơn thì sao , 🔼 📅 2026-07-06 ✅ 2026-07-06

----------------------------------------------------------------------

## ✅ Tasks
- [x] Rà soát hệ thống và kiểm tra thông luồng với các service khác #doing 📅 2026-07-01 ✅ 2026-07-06
- [x] Bàn giao hệ thống cho C Duyên test / ⏫ 📅 2026-07-06 ✅ 2026-07-06
	- [x] Setup data test 📅 2026-07-06 ✅ 2026-07-06
	- [x] Tích hợp thông báo telegram / ⏫ 📅 2026-07-06 ✅ 2026-07-07
	- [x] Sửa lại API web hook cho a Trường đồng nhất message lỗi / 📅 2026-07-07 ✅ 2026-07-07
	- [x] Sửa lại phần đặt lịch luồng khi đặt lịch mà lại thêm giỏ hàng là sai / ⏫ 📅 2026-07-07 ✅ 2026-07-07
	- [x] Fix bug lỗi item ở giỏ hàng bị nhảy index khi add item không thành công / 🔼 📅 2026-07-07 ✅ 2026-07-11
	- [x] API wehook trả cho a Trường 2 field orderNo để lưu và QR khi thanh toán / 🔼 📅 2026-07-09 ✅ 2026-07-10
	- [x] Sửa lại màn hình đặt lịch theo UI Mến sửa 🔼 📅 2026-07-09 ✅ 2026-07-14
- [x] Phân chia outlet theo telegram ⏫ 📅 2026-07-14 ✅ 2026-07-20
- [x] Sửa lại action đồng bộ POS  trong telegram ⏫ 📅 2026-07-14 ✅ 2026-07-20
- [x] Bỏ item khi Đặt lịch / ⏫ 📅 2026-07-14 ✅ 2026-07-14
- [x] Tạo CURL sang POS để check cho dễ trên CMS 🔼 📅 2026-07-14 ✅ 2026-07-14
- [x] Tạo tool import outlet, món ă 🔼 📅 2026-07-14 ✅ 2026-07-17
- [x] Tạo trang bảo trì ⏫ 📅 2026-07-14 ✅ 2026-07-17
- [x] Kiểm tra Đặt chỗ không được quá sức chứ ⏫ 📅 2026-07-14 ✅ 2026-07-17
- [x] Mã code đang hiển thị sai khi có location code rồi 🔼 📅 2026-07-14 ✅ 2026-07-17
- [x] https://jira.apecgroup.net/browse/MC-57 ⏫ 📅 2026-07-17 ✅ 2026-07-20
- [x] Tích hợp môi trường lên PROD ✅ 2026-07-18
- [ ] [ ] Task test 🛫 2026-07-08 📅 2026-07-12






## QUESTION
- khách thanh toán trước đơn -> muốn sửa trực tiếp đơn 
- khách chỉ có thể thanh toán được khi mà nhà hàng hoàn toàn đáp ứng được
? muốn sửa lại đơn trước khi thanh toán 
khách tự thanh toán => đóng bàn => in ra bill
thêm thanh toán pos vào phòng, và chỉ mở cho room service
