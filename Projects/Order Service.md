---
area: "[[Công việc]]"
status: in-progress
...
---

## 📋 Tài liệu

### 🔗 Links
- Prototype Design v1: [Visily](https://app.visily.ai/projects/.../boards/2649806)
- Link Design figma v2: [figma](https://www.figma.com/design/hxt1PmzKzkcmUmzlgMZDwM/Order-Service?node-id=513-8100&t=GiKzjPOOLb3442fy-0\)
- Tài liệu API POS docs: [Google Doc](https://docs.google.com/document/d/1V3m2pImb1asm99cfMjtF-ZoWLBBg9N1K)
- SRS: [Larksuite](https://ujbc4oj6ouc.sg.larksuite.com/docx/CJDrdUMrQoQ4SWxNu3blFoZegpN)
- Tài liệu webhook → POS: [Drive](https://drive.google.com/file/d/1oUXiyFyr0fpy2uoIu9F0Fqr9mw9uIuMj/view)
- Source git: [Git](https://github.com/APECGROUP/Fourier.Lotus.OrderApp)
* Tài liệu khai báo tham số zalo [link](https://docs.google.com/spreadsheets/d/194QakQm8icsabGJ68vMLgmTtJn3cJBvnDfdGW3At4vE/edit?gid=639151913#gid=639151913)
* Check log server: [argo](https://argocd.fourier.group/applications/dev-lotus-order-api-service?node=%2FPod%2Fdev%2Flotus-order-api-service-6c455bb788-jmk6g%2F0&tab=logs&resource=)
* dịch: https://www.deepl.com/en/your-account/keys 

### 🔑 Môi trường TEST
| Hệ thống  | URL                                                            | Tài khoản           | Mật khẩu   |     |
| --------- | -------------------------------------------------------------- | ------------------- | ---------- | --- |
| Web app   | [link](https://order-app-test.lotussolution.cloud/home)        | 0912312312          | room: 2614 |     |
| CMS       | [link](https://order-app-cms-test.lotussolution.cloud/)        | admin@mandala.local | 12345aA@   |     |
| POS       | [link](https://sh-test.qcloud.asia/POS/#/module/03201.MMN)     | admin               | 123123@123 |     |
| XLITE     | [link]( https://xlite-pms-test.lotussolution.cloud/auth/login) | mdlorderadmin       | 12345aA@   |     |
| E-VOUCHER | [link](https://evoucher-test.qcloud.asia/#/module/03100.MMN)   | admin               | 123123     |     |
### 🔑 Môi trường PILOT

| Hệ thống          | URL                                                                 | Tài khoản | Mật khẩu |     |     |
| ----------------- | ------------------------------------------------------------------- | --------- | -------- | --- | --- |
| Khách sạn Kim Bôi | [link](https://order-app.lotussolution.cloud?hotelCode=MDLKB)       |           |          |     |     |
| Khách sạn Mũi né  | [link](http://muine.order-app.mandalahotel.com.vn/?hotelCode=MDLMN) |           |          |     |     |
| CMS               | [link](https://order-app-cms.lotussolution.cloud/)                  | duyenpham | 12345aA@ |     |     |
| POS               |                                                                     |           |          |     |     |
| E-VOUCHER         |                                                                     |           |          |     |     |
### 🔑 Mã group telegram các khách sạn

<table>
  <thead>
    <tr>
      <th>Khách sạn / Resort</th>
      <th>Outlet (Tên nhóm)</th>
      <th>ID Telegram</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Mũi Né</td>
      <td>Mũi Né – Room Service</td>
      <td><code>-5590778913</code></td>
    </tr>
    <tr>
      <td>Mũi Né – Spa</td>
      <td><code>-5543015360</code></td>
    </tr>
    <tr>
      <td rowspan="3"><b>Kim Bôi</b></td>
      <td>Kim Bôi - Room service</td>
      <td><code>-5236458127</code></td>
    </tr>
    <tr>
      <td>Kim Bôi – Spa</td>
      <td><code>-1004360785242</code></td>
    </tr>
    <tr>
      <td>Kim Bôi – Workshop</td>
      <td><code>-5526972260</code></td>
    </tr>
    
    
  </tbody>
</table>
---

## ⚠️ Nợ kỹ thuật
- [ ] Hardcode hotelCode trong source, cần config hóa từ env #techdebt 🔽
- [ ] Tạo doc API CMS #techdebt 🔽
- [x] Phải thay tích hợp XLITE sang domain thật, hiện tại đang dùng mt test của XLITE để golive xong ✅ 2026-09-08


NOTE OT:


17/18 - OT 3 tiếng tích hợp golive mũi né




--------------_CURL

* Thông báo zalo

curl --location 'https://order-app-cms-test.lotussolution.cloud/api/v1/pos/payment-qr-success' \
--header 'Content-Type: application/json' \
--header 'x-api-key: ebfc76f89afc0244e5477efbafeccd197eed557da652ad9ed06cd45282665b2a' \
--data '{
    "orderNo": "FR260706#0032",
    "hotelCode": "MDLMN"
}'

* Tích hợp zalo
curl --location 'https://novu.fourier.group/api/v1/events/trigger' \
--header 'Authorization: ApiKey [key]' \
--header 'Content-Type: application/json' \
--data '{
  "name": "confirm-payment-success",
  "to": {
    "subscriberId": "84332831072",
    "phone": "84332831072"
  },
  "payload": {
    "guestName": "Nguyễn Thành Công",
    "bookingCode": "R.20260101",
    "hotelName": "Mandala Mũi Né",
    "createdAt": "18/08/2026",
    "roomNumber": "TC0001",
    "outlet": "Lễ Tân",
    "paymentStatus": "Thành công",
    "totalAmount": "99.99",
    "__source": "dashboard"
  }
}'
