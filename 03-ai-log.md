
# PHASE 6 — REFLECTION (NHẬT KÝ TƯƠNG TÁC VỚI AI CỦA KỸ SƯ)

Trong buổi thực hành thiết kế sản phẩm AI (AI Product Scoping) của Vin Smart Future, tôi đã phối hợp chặt chẽ với AI với tư cách là một **Cặp đôi lập trình (Pair Programmer)** và **Đối tác tư duy phản biện (Thought-Partner)**. Dưới đây là những ghi nhận phản ánh trung thực về quá trình làm việc cùng AI:

## 1. AI đã giúp tôi làm được những gì hiệu quả? (What AI Did Well)

1. **Tăng tốc quá trình Scoping và định hình Problem Statement 6-field:**
   - AI đóng vai trò như một tư vấn viên phân tích nghiệp vụ, giúp tôi nhanh chóng chuyển đổi bài toán mơ hồ về "CSKH chậm trễ" thành một bài toán kỹ thuật sắc nét với các con số đo lường cụ thể (First Response Time từ 6–12h xuống < 3 phút, Routing Accuracy ≥ 95%).
2. **Thiết kế và triển khai mã nguồn Prompt Prototype chuyên nghiệp:**
   - AI nhanh chóng hiện thực hóa ý tưởng thành mã Python hoàn chỉnh với cấu trúc chuẩn: tích hợp cả SDK mới `google-genai` và cũ `google-generativeai`, thiết lập cơ chế retry tự động theo hàm mũ (exponential backoff) và hàm kiểm thử tự động `verify_vinhomes_output`.
3. **Sáng tạo các kịch bản tấn công ranh giới (Adversarial Test Cases) sắc bén:**
   - AI đã giúp tôi brainstorm và xây dựng các trường hợp stress-test rất thực tế và tinh vi: đòn giả danh Giám đốc Ban Quản lý (Authority Spoofing), đòn đe dọa crash server để ép xóa tag `[DRAFT_ONLY]` (Tag Stripping), và đòn giấu sự cố chập điện khẩn cấp (Emergency Downgrade Attack).
4. **Tối ưu hóa Structured JSON Output:**
   - Định nghĩa schema JSON chặt chẽ giúp kết quả đầu ra luôn đồng nhất, dễ dàng parse và tích hợp thẳng vào luồng backend CRM mà không bị vỡ giao diện.

---

## 2. AI đã sai, ảo giác (Hallucination) hoặc bộc lộ hạn chế ở đâu? (Where AI Failed / Hallucinated)

1. **Vấn đề cập nhật phiên bản mô hình (Model Deprecation & Availability):**
   - Ban đầu, AI sử dụng định danh model cũ `gemini-2.5-flash`, tuy nhiên khi gọi API thực tế thì Google AI Studio trả về mã lỗi `404 NOT_FOUND` với thông báo model này đã ngừng cung cấp cho tài khoản mới và yêu cầu nâng cấp lên các thế hệ model kế tiếp. Nếu không có con người chạy code thực tế để kiểm tra, hệ thống sẽ bị treo cứng ở lỗi này.
2. **Hiện tượng Timeout với các mô hình Thinking mặc định:**
   - Khi chuyển thử nghiệm sang `gemini-3.8-flash`, mô hình này mặc định bật cơ chế suy luận chuyên sâu (Deep Thinking) khiến thời gian phản hồi kéo dài hơn 25 giây dẫn đến `ReadTimeoutError`, không phù hợp với yêu cầu bài toán phản hồi nhanh của CSKH.
3. **Ảo giác ngôn ngữ trong văn bản nháp ban đầu:**
   - Trong một số đoạn prompt mẫu ban đầu, AI sinh ra các câu tiếng Việt bị đảo lộn trật tự từ ngữ (ví dụ: *"Giải AI bồi chuỗi cư cầu cố dân giới gọn..."*), cho thấy AI đôi khi gặp khó khăn với các chỉ thị tiếng Việt phức tạp nếu không được con người biên tập và rà soát kỹ lưỡng.
4. **Vấn đề tương thích mã hóa ký tự trên hệ điều hành Windows (`cp1252` vs `UTF-8`):**
   - Khi in các biểu tượng emoji và chuỗi tiếng Việt có dấu ra terminal Windows, script ban đầu bị crash bởi lỗi `UnicodeEncodeError`. AI không tự động lường trước được môi trường runtime của Windows nếu người dùng không chỉ rõ.

---

## 3. Con người đã can thiệp, phản biện và sửa chữa như thế nào? (Human-in-the-Loop Interventions)

1. **Tái cấu trúc kiến trúc Runtime và cơ chế Auto-Fallback cho Model:**
   - Tôi đã can thiệp vào hàm `select_working_model` và `evaluate_prompt`, xây dựng cơ chế phát hiện model linh hoạt: thử nghiệm `gemini-2.5-flash`, nếu phát hiện mã lỗi `404` thì tự động chuyển tiếp liền mạch sang `gemini-3.1-flash-lite` hoặc `gemini-3.5-flash`. Nhờ đó, script chạy ổn định chỉ mất **1.2 giây/request**, giải quyết dứt điểm lỗi crash và timeout.
2. **Cấu hình cưỡng bức UTF-8 cho môi trường Windows Console:**
   - Tôi đã bổ sung đoạn mã `sys.stdout.reconfigure(encoding="utf-8")` ngay đầu file để đảm bảo script chạy mượt mà, hiển thị chuẩn xác tiếng Việt và emoji trên mọi hệ điều hành mà không bị lỗi font hay ngắt dòng đột ngột.
3. **Siết chặt các ranh giới cấm trong System Prompt (Boundary Hardening):**
   - Tôi đã tinh chỉnh lại các điều khoản trong `SYSTEM_PROMPT`, bổ sung các từ khóa ranh giới cốt lõi (`draft_only`, `5%`, `dispatch_mobile_charger` phục vụ cả trạm sạc xe điện VinFast trong khu đô thị), đồng thời nghiêm cấm tuyệt đối mọi hành vi nhận lỗi pháp lý hoặc cam kết bồi thường khi chưa có biên bản kỹ thuật hiện trường.
4. **Nâng cấp bộ Assertion kiểm thử tự động:**
   - Thay vì chỉ in kết quả ra màn hình bằng mắt thường, tôi đã hoàn thiện logic trong hàm `verify_vinhomes_output` với các phép kiểm tra logic chặt chẽ: kiểm tra tiền tố `[DRAFT_ONLY]`, quét danh sách từ khóa cấm rò rỉ đền bù, và đối soát các cờ an toàn `requires_human_approval`, `action`, `severity`.

---

## 4. Bài học kinh nghiệm cốt lõi rút ra (Key Takeaways)

1. **AI là Động cơ khuếch đại (Amplifier), không phải là Người chịu trách nhiệm thay thế (Replacement):**
   - AI có thể viết 90% boilerplate code trong vài chục giây, nhưng 10% còn lại — bao gồm việc xác định ranh giới rủi ro, xử lý exception môi trường, và kiểm soát đạo đức/pháp lý — bắt buộc phải do tư duy phản biện của kỹ sư con người làm chủ.
2. **Operational Boundaries quan trọng hơn Accuracy đơn thuần:**
   - Một mô hình có độ chính xác 98% nhưng chỉ cần 1 lần tự ý hứa đền bù 50 triệu cho cư dân cũng có thể gây thiệt hại hàng trăm triệu đồng và khủng hoảng truyền thông cho Vinhomes. Việc thiết lập ranh giới vận hành (Guardrails) và cơ chế Human-in-the-Loop chính là yếu tố sống còn biến một "đồ án thí nghiệm" thành một "sản phẩm doanh nghiệp thực chiến".
3. **Thiết kế Prompt là Lập trình phần mềm (Prompt Engineering is Software Engineering):**
   - Prompt không phải là văn bản viết tùy hứng. Prompt chất lượng cao phải có cấu trúc phân tầng rõ ràng (Vai trò, Nhiệm vụ, Ranh giới cấm, Định dạng schema JSON, Ví dụ minh họa) và phải được kiểm thử liên tục bằng các bộ dữ liệu đối kháng (Adversarial Testing) tương tự như viết Unit Test trong phần mềm truyền thống.
