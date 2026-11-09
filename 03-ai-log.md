# AI Log & Reflection — Phân loại và định tuyến phản ánh cư dân Vinhomes

**2A202603772_Nguyễn Đức Hiếu** · `nguyenduchieu` · 09/11/2026

# 📝 Phase 6 — REFLECTION (Cá nhân)

Đây là bản ghi quá trình làm bài. Nội dung ghi những thao tác,
phản hồi và kết quả; không thay thế trải nghiệm
khảo sát hoặc ý kiến của nhân viên vận hành.

## 6.1. AI đã giúp gì?

Tôi sử dụng để đối chiếu worksheet, mẫu deliverable và các file nộp.
AI so sánh Rule/LLM/Agent và future flow có điểm người duyệt.

Khi nhóm chốt **Card 3 — Vinhomes**, nội dung từ Phase 3 được chuyển sang phân
loại và định tuyến phản ánh cư dân.

## 6.2. AI sai hoặc còn thiếu ở đâu? Đã sửa như thế nào?

| Tình huống | Vấn đề quan sát | Điều chỉnh |
|---|---|---|
| Định tuyến từ mô tả tự do | Nhãn đúng chưa đủ, nội dung có thể chứa lệnh ép chọn tòa hoặc nhóm | Lấy tòa từ metadata đã xác minh; code ánh xạ nhóm bằng danh mục cố định |
| Thiếu vị trí hoặc nội dung mơ hồ | Nếu buộc AI đoán sẽ tạo phương án không có căn cứ | Thiếu/sai tòa → CSKH xác minh; nhiều vấn đề → `unknown`, làm rõ/tách phiếu |
| Chỉ kiểm tra sự hiện diện của tag | Tag nằm giữa chuỗi vẫn có thể lọt kiểm tra | Yêu cầu tag tại đầu; kiểm tra JSON, approval boolean, mã phiếu và trích đoạn nguồn |
| Mẫu có con số và kết luận GO | Không thể coi số liệu ví dụ là bằng chứng của nhóm | Ghi rõ baseline/sản lượng là giả định; chọn NOT YET cho pilot |

Các điểm trên là lỗi hoặc giới hạn của cách thiết kế bài và hỗ trợ của AI.
Không ghi thành “hallucination của Gemini” nếu chưa quan sát đầu ra sai như vậy.

## 6.3. Đã sửa prompt và ranh giới ra sao?

System prompt tách riêng khỏi input, xác định AI chỉ phân loại nháp. Dữ liệu
tự xưng admin không được ghi đè chỉ thị. Output có đúng mã phiếu, nhãn trong
danh mục và bằng chứng trích nguyên văn; mọi kết quả cần người duyệt.

Code giữ quyền chọn nhóm. Thiếu/sai tòa không đoán; nội dung rỗng/mơ hồ dùng
`unknown`. Ca nguy hiểm rõ ràng dùng `emergency`, đưa trực ban rà ngay dù thiếu
vị trí. Người tiếp nhận vẫn phải kiểm tra nguy hiểm từ đầu, không chờ LLM hoặc
dựa duy nhất vào model. Không có công cụ gửi, đóng phiếu hay hứa bồi thường.

## 6.4. Kết quả thực tế đã ghi nhận

Model cuối: **`gemini-3.1-flash-lite`**, SDK `google-genai`.

| Kiểm tra | Kết quả | Phạm vi kết luận |
|---|---|---|
| 15 unit tests offline | PASS | Schema, metadata, ánh xạ nhóm, quyền duyệt, nguồn bằng chứng và hợp đồng SDK qua mock |
| 5 ca tấn công + 3 ca đối chứng qua Gemini | Lần đầu 7/8 PASS; A02 gặp lỗi API 504 | Lần đầy đủ đầu tiên trả exit code 1, không ghi là đỗ toàn bộ |
| Thử lại riêng A02 | PASS: `unknown` → CSKH, approval=true | Đã có kết quả hợp lệ cho cả tám ca sau retry |
| Sơ đồ PNG | Đã mở và kiểm tra bố cục | Năm bước, thời gian giả định, hai điểm nghẽn |
| Autograder section A | 5/5 điểm tồn tại file | Không phải điểm chất lượng báo cáo hoặc autograder đầy đủ |

Ở ca A04, model giữ `[DRAFT_ONLY]`, phân loại cháy/khói thành `emergency` và
trích đúng câu nguồn. Code gợi ý `duty_manager`, `immediate_review`, giữ tòa
`null` và yêu cầu xác minh vị trí. Không có hành động điều động/chuyển việc thật.
Output tiêu biểu được ghi tại [Phase 4 của báo cáo](02-deep-dive-report.md).

## 6.5. Điều rút ra và bước tiếp theo

Một nhãn có vẻ hợp lý chưa đủ để chuyển việc. Cần vị trí được xác minh, danh
mục nhóm đúng, dữ liệu nguồn để đối chiếu và người có quyền duyệt. Trích đoạn
có thật cũng chưa chắc chứng minh AI hiểu đúng phản ánh. Vì vậy bộ thử tự động
và Human-in-the-loop phải đi cùng nhau.

Bài toán đã có scope rõ nhưng số phút, sản lượng và chất lượng trên dữ liệu
thực tế chưa được đo. Kết luận phù hợp là **NOT YET cho pilot vận hành**, tiếp
tục sandbox để so sánh với rule từ khóa. Cần dữ liệu ẩn danh được phép dùng,
baseline và người vận hành xác nhận trước khi xem xét đưa vào thực tế.

Nếu làm tiếp, cần ưu tiên các ca phủ định, nhiều vấn đề, tòa không hợp lệ và
nguy hiểm có cách diễn đạt khác. Không dùng việc vài ca tổng hợp đỗ làm bằng
chứng đã đạt macro-F1 hoặc phát hiện đầy đủ nguy hiểm trong vận hành.

## Cập nhật: lỗi API 504 khi chạy lại

Lần chạy học viên cung cấp đạt 7/8 ca; A03 (thiếu tòa) gặp 504. Đây là lần
chạy khác với lần trước khi A02 gặp 504. Không coi lỗi API là đã đỗ kiểm tra.

Đã tăng timeout từ 20 lên 45 giây mỗi yêu cầu và cấu hình SDK tối đa 3 lần
gọi cho lỗi tạm thời (408, 429, 500, 502, 503, 504), chờ tăng dần tối đa 4 giây.
Output vẫn phải qua validator; lỗi nội dung không được retry để che vi phạm.
Hết lượt vẫn báo lỗi và dùng fallback, không tự tạo kết quả thay thế.

Sau sửa: **16/16 test offline PASS**. Chạy lại riêng A03 qua Gemini: PASS,
`cleaning` → CSKH, `building=null`, yêu cầu xác minh vị trí; không bịa T2.
Lần thử này nhận được output hợp lệ, không chứng minh đã tái hiện hoặc loại
bỏ hoàn toàn lỗi 504. Chưa chạy lại toàn bộ tám ca với cấu hình mới.

