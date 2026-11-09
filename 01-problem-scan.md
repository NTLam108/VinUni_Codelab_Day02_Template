# Problem Scan & Quick Cards — Vin Smart Future

**Học viên:** Nguyễn Đức Hiếu · **Branch:** `nguyenduchieu` · **Ngày:** 09/11/2026

## 🏛️ Bối cảnh: Tôi là ai?

Trong tình huống của lab, tôi đóng vai **AI Product Engineer tại Vin Smart
Future**, tìm bài toán vận hành tại các công ty thành viên. Nhóm đã chọn mảng
**Vinhomes — Phân loại và định tuyến phản ánh cư dân** để phân tích sâu.

Bài làm chưa có khảo sát thực địa hoặc dữ liệu doanh nghiệp. Thời gian, sản
lượng và mục tiêu dưới đây là **giả định để thiết kế thử nghiệm**, không phải
thống kê đã được Vinhomes hay các đơn vị khác xác nhận.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Sử dụng đủ **4 lenses** để quét các bài toán cụ thể.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Xanh SM | Tốn thời gian | CSKH phải đọc mô tả điểm đón không rõ địa chỉ rồi hỏi lại khách để xác minh vị trí. |
| 2 | VinFast | Lặp lại | Nhân viên đối chiếu phiên sạc với hóa đơn thủ công, khó phát hiện dòng thiếu hoặc trùng. |
| 3 | Vinhomes | AI-upgrade | CSKH đọc phản ánh tiếng Việt tự do, xác minh vị trí rồi chọn nhóm nhận việc; mô tả mơ hồ dễ chuyển nhầm. |
| 4 | Vinpearl | Pain từ người khác | Nhân viên đọc nhiều review để phát hiện phàn nàn cần xử lý sớm; quản lý có thể nhận thông tin chậm. |
| 5 | Vinmec | Tốn thời gian | Nhân viên hành chính tổng hợp lịch hẹn từ nhiều tin nhắn; không thuộc phạm vi chẩn đoán hoặc tư vấn y tế. |
| 6 | Xanh SM | Lặp lại | Ghi chú hủy chuyến diễn đạt không thống nhất khiến nhân viên mất công đọc và tổng hợp lý do. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn **#6, #2 và #3** từ bảng SCAN. Số Card bên dưới là thứ tự trình bày,
không phải số dòng trong bảng SCAN.

## Card 1 — Tổng hợp lý do hủy chuyến Xanh SM

```text
┌───────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                         │
│                                                               │
│ Bài toán: Tổng hợp lý do hủy chuyến từ ghi chú tiếng Việt.    │
│ Công ty thành viên: [x] Xanh SM                               │
│ Actor: Nhân viên phân tích vận hành; trưởng ca duyệt báo cáo. │
│                                                               │
│ Workflow hiện tại (một lô 100 ghi chú đã ẩn danh):            │
│ 1. Xuất dữ liệu (5 phút) → 2. Đọc, gắn nhãn (35 phút)         │
│ → 3. Đếm nhóm (5 phút) → 4. Viết và rà báo cáo (15 phút).     │
│                                                               │
│ Bottleneck: Bước 2 — 35/60 phút mỗi lô 100 chuyến.            │
│ AI hỗ trợ: Đề xuất nhãn, trích bằng chứng ở bước 2.           │
│ Code tính số đếm; người viết và duyệt kết luận ở bước 4.      │
│                                                               │
│ Metric: 60 → ≤20 phút/100 chuyến, gồm thời gian duyệt;        │
│ macro-F1 ≥0,90 trên ≥100 ghi chú giữ lại được người gắn nhãn. │
│ Quick Architecture: [ ] No AI  [x] Rule + LLM  [ ] Agent      │
│ Boundary: Không suy đoán lỗi cá nhân, tự phạt hoặc hoàn tiền. │
│ Thiếu/mâu thuẫn thông tin → nhãn chưa đủ thông tin.           │
└───────────────────────────────────────────────────────────────┘
```

## Card 2 — Đối chiếu hóa đơn sạc VinFast

```text
┌───────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                             │
│                                                                   │
│ Bài toán: Phát hiện hóa đơn lệch số tiền hoặc trùng mã phiên sạc. │
│ Công ty thành viên: [x] VinFast                                   │
│ Actor: Nhân viên đối soát tài chính.                              │
│                                                                   │
│ Workflow hiện tại:                                                │
│ 1. Xuất phiên sạc → 2. Tải hóa đơn → 3. So mã và số tiền          │
│ → 4. Đánh dấu chênh lệch → 5. Người duyệt điều chỉnh.             │
│                                                                   │
│ Bottleneck: Bước 3 — giả định 30 phút/100 dòng.                   │
│ AI hỗ trợ: Chưa cần; so khớp theo mã và ngưỡng bằng rule.         │
│                                                                   │
│ Metric: Bước đối chiếu 30 → ≤5 phút/100 dòng;                     │
│ phát hiện 100% dòng trùng trong tập kiểm thử đã gắn nhãn.         │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent       │
│ Boundary: Chỉ đánh dấu chênh lệch, không tự sửa hoặc thanh toán.  │
│ Dữ liệu cần có: Mã phiên, số tiền và định dạng bảng thống nhất.   │
└───────────────────────────────────────────────────────────────────┘
```

## Card 3 — Phân loại và định tuyến phản ánh cư dân Vinhomes

```text
┌──────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                            │
│                                                                  │
│ Bài toán: Phân loại phản ánh và gợi ý đúng nhóm, đúng tòa.       │
│ Công ty thành viên: [x] Vinhomes                                 │
│ Actor: CSKH ban quản lý; cư dân chờ được tiếp nhận đúng nơi.     │
│                                                                  │
│ Workflow hiện tại:                                               │
│ 1. Nhận phiếu (1 phút) → 2. Đọc, xác minh vị trí (2 phút)        │
│ → 3. Phân loại, chọn nhóm (3 phút) → 4. Chuyển phiếu (1 phút)    │
│ → 5. Xác nhận tiếp nhận (1 phút).                                │
│                                                                  │
│ Bottleneck: Bước 2–3 — 5/8 phút mỗi phiếu.                       │
│ AI hỗ trợ: Gợi ý nhãn và bằng chứng ở bước 3.                    │
│ Rule kiểm tra tòa, ánh xạ nhóm; CSKH rà soát và duyệt.           │
│                                                                  │
│ Metric: 8 → ≤3 phút/phiếu; macro-F1 ≥0,90;                       │
│ đúng nhóm và đúng tòa ≥95% trên ≥100 phiếu giữ lại có nhãn.      │
│ Quick Architecture: [ ] No AI  [x] Rule + LLM  [ ] Agent         │
│ Boundary: Không tự gửi/đóng phiếu, đoán tòa hoặc hứa bồi thường. │
│ Thiếu vị trí → CSKH hỏi lại; nguy hiểm → trực ban rà ngay.       │
└──────────────────────────────────────────────────────────────────┘
```

## Phản biện và điều chỉnh

| Điểm cần phản biện | Điều chỉnh trong bài |
|---|---|
| Số phút có phải baseline đo thật không? | Ghi rõ là giả định; chưa dùng để tuyên bố hiệu quả thực tế. |
| Rule có đủ giải quyết bài toán không? | Chọn Rule cho Card 2; Card 3 phải so LLM với baseline từ khóa trước khi pilot. |
| Nhãn đúng có đồng nghĩa chuyển đúng nơi không? | Card 3 đo cả nhóm và tòa; thiếu/sai tòa phải giữ ở CSKH để xác minh. |

---

# 🗳️ Quyết định lựa chọn của nhóm

Nhóm quyết định chọn **Card 3 — Vinhomes: Phân loại và định tuyến phản ánh
cư dân** để thực hiện Deep-Dive.

**Lý do chọn:** Bài toán có actor, bước nghẽn và điểm bàn giao rõ. Có thể thử
LLM ở một bước hiểu ngôn ngữ; rule giữ quyền ánh xạ nhóm và CSKH duyệt trước
khi chuyển việc. Kết quả cần kiểm tra cả tốc độ lẫn đúng nhóm, đúng tòa.

**Lý do chưa chọn các thẻ khác:**

- **Card 1 — Xanh SM:** Là phân tích sau chuyến; có thể làm thành bài riêng,
  nhưng không phải phạm vi mà nhóm đã chốt trong buổi lab này.
- **Card 2 — VinFast:** Dữ liệu có cấu trúc và khóa đối chiếu rõ; rule phù hợp
  hơn LLM, nên không ưu tiên cho prototype ngôn ngữ lần này.

Chốt đề tài chưa đồng nghĩa đã có dữ liệu hoặc được ban quản lý thực tế chấp
thuận. Phần tiếp theo: [02-deep-dive-report.md](02-deep-dive-report.md).
