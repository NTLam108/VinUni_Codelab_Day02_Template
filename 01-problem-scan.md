Phase 1 — SCAN (Cá nhân, 20 min)
📝 List bài toán của tôi:

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
| --- | --- | --- | --- |
| 1 | **VinFast** | Lặp lại / Tốn thời gian | Thẩm định & phân loại tự động hồ sơ bảo hành phụ tùng/pin (Warranty Claims Triage) kết hợp đối soát mã lỗi OBD và phát hiện gian lận bảo hành. |
| 2 | **Xanh SM** | Pain từ người khác | Điều phối thông minh trạm sạc V-GREEN cho đội xe cạn pin (<10% SoC) theo thời gian thực thay vì gọi tổng đài hỗ trợ thủ công. |
| 3 | **Vinhomes** | AI-upgrade / Tốn thời gian | Phân luồng đa nhãn tự động, đánh giá mức độ nghiêm trọng và sinh bản nháp phản hồi cá nhân hóa cho phản ánh cư dân trên App Vinhomes Resident. |
| 4 | **Vinmec** | Pain từ người khác | Tự động tổng hợp dữ liệu EMR/HIS và trích xuất mã ICD để sinh biên bản tóm tắt hồ sơ xuất viện cho bác sĩ lâm sàng. |
| 5 | **Xanh SM** | AI-upgrade / Tốn thời gian | Phân tích tự động nguyên nhân gốc rễ (RCA) cuốc xe bị hủy thông qua chuyển đổi giọng nói (STT) từ cuộc gọi ghi âm và ghi chú của tài xế. |








Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #01                                      │
│                                                             │
│ Bài toán (1 câu): Thẩm định, đối soát mã lỗi OBD và phân    │
│ loại tự động hồ sơ bảo hành phụ tùng/pin xe điện VinFast.   │
│ Công ty thành viên: [X] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Chuyên viên thẩm định bảo hành Hội sở  │
│ & Quản đốc xưởng dịch vụ 3S.                                │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Xưởng tạo claim (ảnh hóa đơn, phụ tùng, ảnh mã OBD)    │
│   ──> 2. Chuyên viên đọc claim, tra cứu mã DTC & telemetry  │
│   ──> 3. Đối soát lịch sử sạc/bảo dưỡng để loại trừ lỗi user│
│   ──> 4. Nhập tay quyết định phê duyệt/từ chối lên SAP/DMS  │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 25 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3 (OCR trích │
│ xuất claim + AI đối soát tự động log xe và điều khoản bh).  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Giảm thời gian duyệt claim từ 25 min ──> under 3 min/ca │
│   - Tự động hóa phê duyệt (Auto-approval rate) đạt 70%      │
│   - Giảm tỷ lệ duyệt sai/gian lận bảo hành từ 4% ──> under 1%│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [X] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #02                                      │
│                                                             │
│ Bài toán (1 câu): Tối ưu định tuyến và đặt trước slot sạc   │
│ thời gian thực cho đội xe Xanh SM sắp cạn pin (<10% SoC).   │
│ Công ty thành viên: [ ] VinFast  [X] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế taxi Xanh SM & Điều phối viên   │
│ hỗ trợ khẩn cấp tổng đài.                                   │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Xe báo pin cạn (<10%), tài xế gọi hotline khẩn cấp     │
│   ──> 2. Điều phối viên mở bản đồ V-GREEN dò tìm trụ trống   │
│   ──> 3. Điều phối viên gọi/nhắn hướng dẫn tài xế chạy đến  │
│   ──> 4. Tài xế đến nơi, nếu trạm kín chỗ phải gọi lại từ đầu│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 15 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3 (Hệ thống  │
│ tự động tính toán SoC, cự ly và giữ chỗ slot sạc tối ưu).    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   - Giảm thời gian tìm và tiếp cận trạm sạc từ 35 min ──> 12 min│
│   - Giảm 100% cuộc gọi điều phối thủ công về pin cạn        │
│   - Tăng sản lượng xe hoạt động thêm 45.000 giờ lăn bánh/tháng│
│                                                             │
│ Quick Architecture: [ ] No AI  [X] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #03                                      │
│                                                             │
│ Bài toán (1 câu): Phân loại đa nhãn, xác định mức độ khẩn cấp│
│ và soạn dự thảo phản hồi ticket cư dân trên App Vinhomes.   │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [X] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH/Ban Quản lý tòa nhà     │
│ & Cư dân đại đô thị.                                        │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tiếp nhận text/ảnh phản ánh từ cư dân trên App         │
│   ──> 2. Nhân viên đọc nội dung, gắn tag phân loại thủ công │
│   ──> 3. Forward ticket sang đội Kỹ thuật/An ninh liên quan │
│   ──> 4. Gõ câu trả lời theo văn mẫu thủ công cho cư dân     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 12 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Toàn bộ bước 2, 3, 4  │
│ (Phân loại tự động, route đúng đội và sinh nháp câu trả lời)│
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   - Rút ngắn First Response Time từ 6–12 tiếng ──> under 15 phút│
│   - Giảm tỷ lệ điều phối sai bộ phận từ 15% ──> under 2%     │
│   - Cắt giảm 60% thời gian xử lý sự vụ của nhân sự CSKH Tầng 1│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [X] Agent │
└─────────────────────────────────────────────────────────────┘