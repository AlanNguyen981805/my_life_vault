

> Lĩnh vực: các dự án công ty, freelance, sản phẩm.

## 🚀 Dự án đang chạy

```dataview
TABLE status AS "Trạng thái", due_date AS "Deadline", priority AS "Ưu tiên"
FROM "Projects"
WHERE area = this.file.link AND status != "done"
SORT due_date ASC
```


--------------------------------------------------------
## ✅ Dự án đã xong
```dataview
LIST FROM "Projects"
WHERE area = this.file.link AND status = "done"
```

## 📝 Ghi chú chung