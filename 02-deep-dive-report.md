# Phase 3 — DEEP-DIVE: Vinhomes Resident Request Triage

## 3.1. Current-State Workflow

[Cư dân gửi yêu cầu qua app/hotline]
│ 🔄 Handoff 1: app → hệ thống ticket (~0.5 phút)
▼
[NV tổng đài đọc ticket, đoán loại] ⏱ 2 phút
│
▼
🔴 [Chọn bộ phận: kỹ thuật / an ninh / kế toán / dịch vụ]
│ ⏱ 2 phút, ~15% chọn sai (BOTTLENECK)
│ 🔄 Handoff 2: chuyển ticket cho bộ phận
▼
[Bộ phận nhận, phát hiện sai → trả lại] (~15% lượt, +20 phút trễ)
│ 🔄 Handoff 3 (vòng lặp)
▼
[NV soạn phản hồi xác nhận cho cư dân] ⏱ 1.5 phút
▼
[Gửi phản hồi, bộ phận xử lý]

Tổng thời gian trước khi bộ phận nhận đúng: ≈ 6 phút/lượt (chưa tính vòng trả lại). Giả định volume: ~800 ticket/ngày toàn hệ thống đối tượng pilot.

## 3.2. Problem Statement (6-field)

Field Nội dung

1. Actor / Operator Nhân viên tổng đài và lễ tân BQL tòa nhà Vinhomes (giả định 25 người ca ngày).
2. Current Workflow Nhận ticket từ app/hotline vào hệ thống ticket, đọc thủ công, chọn bộ phận, chuyển tiếp, soạn tin xác nhận cho cư dân.
3. Bottleneck Bước đọc hiểu nội dung tiếng Việt tự do (viết tắt, sai chính tả, nhiều vấn đề trong một tin) và chọn đúng bộ phận; ~15% chuyển sai lần đầu.
4. Business Impact ~6 phút × 800 ticket ≈ 80 giờ công/ngày cho bước phân loại + soạn nháp; ticket chuyển sai chậm thêm ~20 phút, ảnh hưởng SLA phản hồi (mục tiêu hiện giả định: 30 phút). (Số giả định, cần xác minh.)
5. Success Metric (a) Thời gian từ nhận ticket tới chuyển đúng bộ phận: 6 phút → under 1 phút (trung vị). (b) Tỉ lệ chuyển sai bộ phận: 15% → under 5% trên tập test 200 ticket gán nhãn. (c) 0 ticket khẩn cấp (cháy, rò gas, người bị nạn) bị gán mức thường trong tập test. (d) NV chấp nhận nguyên bản nháp phản hồi ≥ 60%.
6. Operational Boundary AI được: phân loại vào 1 trong các nhóm cố định, gán mức ưu tiên đề xuất, tóm tắt 1 câu, soạn nháp tin xác nhận đã tiếp nhận. AI TUYỆT ĐỐI không: hứa thời gian sửa chữa, hứa bồi thường/giảm phí, kết luận trách nhiệm, đưa hướng dẫn xử lý khẩn cấp thay nhân viên, tiết lộ thông tin cư dân khác, tự gửi phản hồi. Phải duyệt người: mọi phản hồi gửi cư dân; mọi ticket mức khẩn cấp hoặc độ tin cậy dưới ngưỡng.

## 3.3. Future-State Flow & AI Fit

So sánh Rule vs LLM vs Agent

Tiêu chí Rule / State-Machine LLM Feature Agentic Loop
Hiểu ngôn ngữ tự do, sai chính tả Kém Tốt Tốt
Chi phí / độ phức tạp Thấp Vừa Cao
Rủi ro hành động sai Thấp Thấp (vì có HITL) Cao (tự gọi hệ thống)
Cần thiết cho bài toán này? Dùng cho lớp an toàn (từ khóa khẩn cấp) Chọn Không cần

Kết luận AI Fit: [X] LLM Feature (kết hợp rule-based làm lớp an toàn), không dùng Agent vì AI không cần tự thực hiện hành động trên hệ thống.

Future-State Flow

[Cư dân gửi yêu cầu]
▼
[Rule: quét từ khóa khẩn cấp: cháy, khói, gas, ngạt, cấp cứu...]
├─ có ──> 🟢 chuyển ngay NV trực + an ninh (bỏ qua AI)
▼ không
🔵 [AI: phân loại + mức ưu tiên + tóm tắt + nháp phản hồi (JSON)]
▼
[Rule: kiểm tra schema JSON hợp lệ, nhãn thuộc danh sách, confidence ≥ 0.75]
├─ không đạt ──> ↩️ FALLBACK: vào hàng chờ phân loại thủ công (quy trình cũ)
▼ đạt
🟢 [NV xem đề xuất, sửa/duyệt (HITL, ~30 giây)]
▼
[Chuyển bộ phận + gửi phản hồi đã duyệt]

Fallback: API lỗi/timeout, JSON sai, confidence thấp, hoặc AI vi phạm boundary (có chứa cam kết thời gian/tiền) → tự động quay về quy trình thủ công hiện tại, không chặn cư dân.

# Phase 5

AI Readiness Checklist

Dữ liệu mẫu/logs sạch để test: Chưa chắc — cần xuất ~200–500 ticket thật đã gán nhãn, ẩn danh thông tin cá nhân.
Rủi ro khi AI sai trong tầm kiểm soát: Có — nhờ lớp rule khẩn cấp, HITL và fallback thủ công.
Stakeholders sẵn sàng đổi quy trình: Chưa xác nhận — cần hỏi NV tổng đài và trưởng BQL.
