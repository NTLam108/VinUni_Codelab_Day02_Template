# 🔍 Phase 1 — SCAN 
### 📝 List bài toán của tôi:
| # | Subsidiary | Tên bài toán / Bottleneck | Lens | Mô tả ngắn |
|---|------------|---------------------------|------|------------|
| 1 | **Vin Fast** | Tìm kiếm và gợi ý trạm sạc | Tốn thời gian | Tối ưu hóa lịch trình và địa điểm sạc taxi điện dựa trên SOC pin, vị trí/lộ trình xe và tình trạng khả dụng của trạm sạc. Tự động cảnh báo khi pin dưới 40% và đề xuất trạm sạc, thời điểm và lộ trình phù hợp nhằm giảm thời gian chờ, quãng đường di chuyển phát sinh và gián đoạn khai thác xe. |
| 2 | **Xanh SM** | Dự báo nhu cầu và phân bổ tài xế | AI có thể tốt hơn | Dự báo nhu cầu đặt xe theo khu vực và khung giờ dựa theo lịch sử, kết hợp vị trí tài xế để đề xuất phân bổ và điều phối xe tối ưu, giảm tình trạng thiếu/thừa xe cục bộ, thời gian chờ và chuyến xe rỗng. |
| 3 | **VinFast** | Tự động xử lý yêu cầu bảo hành | Tốn thời gian | Trích xuất thông tin từ phiếu bảo hành, hình ảnh, mô tả lỗi và lịch sử sửa chữa để phân loại yêu cầu, kiểm tra điều kiện bảo hành và đề xuất hướng xử lý ban đầu. |
| 4 | **Vinhomes** | Trợ lý AI tra cứu thông tin cư dân | AI có thể tốt hơn | Xây dựng trợ lý RAG giúp cư dân tra cứu quy định, phí dịch vụ, tiện ích, hướng dẫn sử dụng và gửi yêu cầu hỗ trợ bằng ngôn ngữ tự nhiên. |
| 5 | **Vinmec** |  Trợ lý AI tổng hợp hồ sơ bệnh án | Tốn thời gian | Tự động tổng hợp tiền sử bệnh, kết quả xét nghiệm, thuốc đang sử dụng và các lần khám trước thành bản tóm tắt để bác sĩ tham khảo. |

# 🃏 Phase 2 — QUICK-ASSESS

```
┌──────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                │
│                                                                      │
│ Bài toán (1 câu): Tìm kiếm và gợi ý trạm sạc                         │
│ Công ty thành viên: [ x ] VinFast  [ ] Xanh SM  [ ] Vinhomes         │
│                      [ ] Vinmec  [ ] Khác (Ghi rõ)________           │
│                                                                      │
│ Ai đang đau (Actor)? Người dùng xe / Tài xế                          │
│                                                                      │
│ Workflow thủ công hiện tại (3-5 bước):                               │
│   1. Kiểm tra mức pin (SOC) của xe                                   │
│   2. Tìm kiếm các trạm sạc gần vị trí hiện tại hoặc điểm đến         │
│   3. Lựa chọn điểm đến và chờ trạm sạc                               │
│                                                                      │
│ Bước nào tốn thời gian/lỗi nhất? 2. Tìm kiếm các trạm sạc gần vị trí │
│ hiện tại hoặc điểm đến và 3. Lựa chọn điểm đến và chờ trạm sạc. (15 - │
│ 30 phút/lượt)                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? 2. Tự động tìm kiếm các trạm   │
│ sạc tại vị trí hiện tại hoặc điểm đến, 3. Đánh giá tình hình và nhu  │
│ cầu của các trạm sạc dựa trên hệ thống để đưa ra gợi ý trạm sạc,     │
│ giảm thời gian đợi sạc                                               │
│                                                                      │
│ Đo thành công bằng gì (Metric có số)?                                │
│ Giảm thời gian tìm kiếm trạm sạc: 5-10 phút -> 2 phút.               │
│ Giảm 20% thời gian chờ sạc                                           │
│                                                                      │
│ Quick Architecture: [ ] No AI  [X] Rule  [ ] LLM  [X] Agent          │
└──────────────────────────────────────────────────────────────────────┘
```

```
┌──────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                │
│                                                                      │
│ Bài toán (1 câu): Dự báo nhu cầu và phân bổ tài xế                   │
│ Công ty thành viên: [ ] VinFast  [ X ] Xanh SM  [ ] Vinhomes         │
│                      [ ] Vinmec  [ ] Khác (Ghi rõ)________           │
│                                                                      │
│ Ai đang đau (Actor)? Tài xế                                          │
│                                                                      │
│ Workflow thủ công hiện tại (3-5 bước):                               │
│   1. Tài xế kiểm tra vị trí và tình trạng hoạt động của xe           │
│   2. Tìm kiếm hoặc di chuyển đến khu vực có khả năng đông khách      │
│   3. Chờ yêu cầu đặt xe và nhận chuyến từ hệ thống                   │
│   4. Tiếp tục di chuyển hoặc thay đổi khu vực khi nhu cầu thấp       │
│                                                                      │
│ Bước nào tốn thời gian/lỗi nhất? 2. Tìm kiếm hoặc di chuyển đến khu  │
│ vực có khả năng đông khách (5 - 10 phút/lượt)                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? 2. Dự đoán nhu cầu đặt xe theo │
│ các khu vực dựa vào lịch sử dữ liệu để gợi ý khu vực gần nhất.       │
│                                                                      │
│ Đo thành công bằng gì (Metric có số)?                                │
│ Giảm 20% thời gian tài xế chờ nhận chuyến                            │
│ Giảm 10% quãng đường xe chạy rỗng.                                   │
│                                                                      │
│ Quick Architecture: [ ] No AI  [X] Rule  [ ] LLM  [X] Agent          │
└──────────────────────────────────────────────────────────────────────┘
```

```
┌──────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                │
│                                                                      │
│ Bài toán (1 câu): Trợ lý AI tổng hợp hồ sơ bệnh án                   │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes           │
│                      [ X ] Vinmec  [ ] Khác (Ghi rõ)________         │
│                                                                      │
│ Ai đang đau (Actor)? Bác sĩ khám bệnh / Bác sĩ điều trị              │
│                                                                      │
│ Workflow thủ công hiện tại (3-5 bước):                               │
│   1. Bác sĩ tìm kiếm và mở hồ sơ bệnh án của bệnh nhân trên hệ thống │
│   2. Tìm và xem lại thông tin từ các lần khám trước, kết quả xét     │
│      nghiệm, chẩn đoán và đơn thuốc                                  │
│   3. Đối chiếu thông tin giữa nhiều tài liệu và hệ thống khác nhau   │
│   4. Tổng hợp tiền sử và tình trạng hiện tại để phục vụ quá trình    │
│      khám, chẩn đoán và điều trị                                     │
│                                                                      │
│ Bước nào tốn thời gian/lỗi nhất? 2. Tìm và xem lại thông tin từ các  │
│ lần khám trước, kết quả xét nghiệm, chẩn đoán và đơn thuốc và 3. Đối │
│ chiếu thông tin giữa nhiều tài liệu và hệ thống khác nhau (5 - 10    │
│ phút/lượt)                                                           │
│ AI có thể nhảy vào hỗ trợ ở bước nào? 2. Tự động đọc và tổng hợp hồ  │
│ sơ bệnh án thành bản tóm tắt có cấu trúc, gồm tiền sử bệnh, chẩn     │
│ đoán trước đây, thuốc đang sử dụng, kết quả xét nghiệm và các diễn   │
│ biến quan trọng, kèm trích dẫn chính xác thông tin gốc. 3. Bác sĩ    │
│ kiểm tra và xác nhận trước khi sử dụng.                              │
│                                                                      │
│ Đo thành công bằng gì (Metric có số)?                                │
│ Giảm 50% thời gian bác sĩ tìm kiếm và tổng hợp hồ sơ.                │
│ Đạt độ chính xác trích xuất thông tin từ 95% trở lên                 │
│                                                                      │
│ Quick Architecture: [ ] No AI  [ ] Rule  [X] LLM  [X] Agent          │
└──────────────────────────────────────────────────────────────────────┘
```
