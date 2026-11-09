# Lab 02 — Worksheet hoàn thiện: AI Product Scoping (Vin Smart Future)

---

## Phase 1 — SCAN (Cá nhân)

| #   | Subsidiary            | Lens                    | Mô tả ngắn bài toán                                                                                                                                                      |
| --- | --------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | Vinhomes              | Lặp lại / Tốn thời gian | Phân loại và định tuyến yêu cầu/khiếu nại của cư dân (thang máy hỏng, rò nước, tiếng ồn, phí quản lý...) gửi qua app/hotline tới đúng bộ phận kỹ thuật, an ninh, kế toán |
| 2   | Xanh SM               | Pain từ người khác      | Tài xế phàn nàn điểm đón khách không chính xác (pin GPS lệch tại cổng tòa nhà lớn, sân bay)                                                                              |
| 3   | VinFast               | Lặp lại                 | Đối soát hóa đơn sạc điện (VinFast Charging) giữa dữ liệu trạm, ví thanh toán và khiếu nại của khách                                                                     |
| 4   | Vinpearl / VinWonders | AI có thể tốt hơn       | Chatbot CSKH đặt vé/đổi vé trả lời rập khuôn, không hiểu câu hỏi nhiều ý (ví dụ đổi ngày + thêm trẻ em + mã khuyến mãi)                                                  |
| 5   | Vinmec                | Tốn thời gian           | Tóm tắt hồ sơ bệnh án dài cho bác sĩ trước buổi tái khám (chỉ tóm tắt, không chẩn đoán)                                                                                  |

---

## Phase 2 — QUICK CARDS (Top 3)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│ Bài toán: Phân loại + định tuyến yêu cầu cư dân tới đúng    │
│           bộ phận xử lý và soạn sẵn phản hồi nháp.          │
│ Công ty: [ ] VinFast [ ] Xanh SM [X] Vinhomes [ ] Vinmec    │
│ Actor: Nhân viên tổng đài/lễ tân Vinhomes (BQL tòa nhà)     │
│ Workflow: 1. Nhận ticket ──> 2. Đọc, đoán loại ──>          │
│           3. Chuyển bộ phận ──> 4. Soạn phản hồi cho cư dân │
│ Bước tốn thời gian/lỗi nhất: Bước 2-3 (đọc + chuyển sai     │
│   bộ phận) ⏱ ~6 phút/lượt, ~15% chuyển sai lần đầu (giả định)│
│ AI nhảy vào ở: Bước 2-3 (phân loại) và 4 (soạn nháp)        │
│ Metric: Giảm thời gian xử lý ban đầu từ 6 phút ──> under 1  │
│   phút; tỉ lệ chuyển sai bộ phận từ 15% ──> under 5%        │
│ Quick Architecture: [ ] No AI [ ] Rule [X] LLM [ ] Agent    │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│ Bài toán: Đối soát khiếu nại hóa đơn sạc điện VinFast.      │
│ Công ty: [X] VinFast [ ] Xanh SM [ ] Vinhomes [ ] Vinmec    │
│ Actor: Nhân viên CSKH / kế toán trạm sạc                    │
│ Workflow: 1. Nhận khiếu nại ──> 2. Tra log phiên sạc ──>    │
│           3. So với giao dịch ví ──> 4. Hoàn tiền/từ chối   │
│ Bước tốn thời gian nhất: Bước 2-3 (tra 2-3 hệ thống)        │
│   ⏱ ~12 phút/lượt (giả định)                                │
│ AI nhảy vào ở: Đọc nội dung khiếu nại, trích mã phiên sạc   │
│   (phần đối soát số liệu nên là code, không phải AI)        │
│ Metric: Thời gian xử lý từ 12 ──> under 4 phút/lượt         │
│ Quick Architecture: [ ] No AI [X] Rule [ ] LLM [ ] Agent    │
│   (đối soát = rule; LLM chỉ hỗ trợ trích thông tin)         │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│ Bài toán: Chatbot CSKH Vinpearl xử lý yêu cầu đổi vé nhiều ý│
│ Công ty: [ ] VinFast [ ] Xanh SM [ ] Vinhomes [ ] Vinmec    │
│          [X] Khác: Vinpearl / VinWonders                    │
│ Actor: Khách mua vé + nhân viên CSKH nhận ca chuyển tiếp    │
│ Workflow: 1. Khách hỏi bot ──> 2. Bot trả lời mẫu, sai ý ──>│
│           3. Khách gọi hotline ──> 4. Nhân viên xử lý lại   │
│ Bước tốn thời gian/lỗi nhất: Bước 2-3 (bot không hiểu →     │
│   chuyển người) ⏱ thêm ~8 phút/lượt (giả định)              │
│ AI nhảy vào ở: Hiểu câu hỏi nhiều ý, tra chính sách, trả lời│
│ Metric: Tỉ lệ bot giải quyết xong không cần người từ 40% ──>│
│   65%, không tăng khiếu nại sai chính sách                  │
│ Quick Architecture: [ ] No AI [ ] Rule [X] LLM [ ] Agent    │
└─────────────────────────────────────────────────────────────┘
```
