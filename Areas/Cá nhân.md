
#  Cá nhân

> Lĩnh vực: phát triển bản thân, kỷ niệm, mối quan hệ, việc nhà.

## 🎯 Mục tiêu cá nhân

```dataview
TABLE status AS "Trạng thái", target_date AS "Hạn"
FROM "Goals"
WHERE area = this.file.link
```

## 🚀 Việc đang làm

```dataview
TABLE status AS "Trạng thái", due_date AS "Deadline"
FROM "Projects"
WHERE area = this.file.link AND status != "done"
```

## 💭 Nhật ký / kỷ niệm

> Link tới các note kỷ niệm, suy nghĩ cá nhân.

## 📝 Ghi chú