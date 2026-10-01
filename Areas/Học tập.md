

> Lĩnh vực: tiếng Anh, kỹ năng lập trình, khóa học.

## 🎯 Mục tiêu dài hạn

```dataview
TABLE status AS "Trạng thái", target_date AS "Hạn"
FROM "Goals"
WHERE area = this.file.link
```

## 🚀 Dự án / khóa học đang chạy

```dataview
TABLE status AS "Trạng thái", due_date AS "Deadline"
FROM "Projects"
WHERE area = this.file.link AND status != "done"
SORT due_date ASC
```

## 📚 Tài nguyên học


## 📝 Ghi chú