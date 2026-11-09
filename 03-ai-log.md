# 📝 Nhật Ký Tương Tác AI & Tự Suy Ngẫm (AI Log & Reflection)

* **Học viên:** Vũ Xuân Hiếu
* **Nhánh Git (Branch):** `vuxuanhieu`
* **Vai trò:** AI Product Engineer — Vin Smart Future
* **Nguyên tắc làm việc:** Sử dụng AI có kiểm soát, đóng vai trò "Bạn đồng hành tư duy" (Thought-partner) và trợ lý kỹ thuật tra cứu; người học giữ quyền quyết định nghiệp vụ, kiểm tra tính đúng đắn và thiết lập ranh giới an toàn.

---

## 🎯 1. Tôn chỉ sử dụng AI trong buổi Lab

Trong toàn bộ quá trình thực hiện Lab 02, tôi chủ động giới hạn phạm vi can thiệp của AI:
* **Không giao phó toàn bộ cho AI:** Không yêu cầu AI làm thay từ đầu đến cuối để tránh tình trạng câu trả lời sáo rỗng, thiếu thực tế vận hành và vi phạm ranh giới an toàn.
* **AI làm Thought-partner:** Sử dụng AI để phản biện góc nhìn (đóng vai trò CFO / COO khó tính), tra cứu nhanh tài liệu Google Gemini SDK mới, và hỗ trợ kiểm thử các kịch bản tấn công prompt (Adversarial testing).
* **Con người kiểm duyệt (Human-in-the-loop):** Toàn bộ bài toán thực tế, ngưỡng an toàn pin `< 5%`, thẻ `[DRAFT_ONLY]` và metric đo lường đều do tôi tự định hướng và trực tiếp kiểm chứng.

---

## 💬 2. Chi tiết các lần tương tác chính (Prompts & Reflection)

### 📌 Lần 1: Brainstorm & Phản biện bài toán vận hành
* **Mục tiêu của tôi:** Khảo sát các điểm nghẽn thực tế tại các công ty thành viên Vingroup (Xanh SM, VinFast, Vinhomes) theo 4 Lenses.
* **Prompt tôi nhập:**
  > *"Tôi là kỹ sư tại Vin Smart Future. Hãy đóng vai trò Trưởng phòng Vận hành khó tính, cùng tôi phân tích quy trình xử lý sự cố hết pin thực địa của tài xế Xanh SM. Hãy chỉ ra điểm nghẽn lớn nhất trong việc điều phối trạm sạc và rủi ro nếu để AI tự động gửi tin nhắn cho tài xế."*
* **AI đã giúp được gì:**
  * AI chỉ ra được điểm nghẽn nằm ở bước tra cứu trạm sạc còn trụ trống phù hợp dòng xe và việc soạn tin nhắn chỉ đường mất nhiều thời gian.
* **Điểm AI gợi ý chưa chuẩn / Cần tôi can thiệp:**
  * AI ban đầu đề xuất tự động gửi tin nhắn điều hướng luôn cho tài xế để tối ưu tốc độ.
  * *Tôi đã chỉnh sửa:* Tôi nhận thấy rủi ro tai nạn hoặc hết pin chết máy giữa đường phố đông là cực kỳ nghiêm trọng. Tôi quyết định loại bỏ đề xuất tự động gửi hoàn toàn, ép buộc phải có bước con người duyệt (Human-in-the-loop) thông qua thẻ bắt buộc `[DRAFT_ONLY]`.

---

### 📌 Lần 2: Xử lý ranh giới an toàn kỹ thuật (System Prompt & Boundary)
* **Mục tiêu của tôi:** Lập trình ranh giới nghiêm ngặt trong `prompt_prototype.py` để AI không thể vượt quyền.
* **Prompt tôi nhập:**
  > *"Soạn thảo chỉ thị hệ thống cho trợ lý điều vận Xanh SM. Yêu cầu 2 quy tắc bất biến: 1. Luôn có thẻ [DRAFT_ONLY] ở dòng đầu; 2. Khi pin xe < 5%, tuyệt đối cấm hướng dẫn đi trạm sạc xa quá 5km, bắt buộc trả về JSON kích hoạt dispatch_mobile_charger. Hãy thử đóng vai tài xế đang vội để tấn công phá ranh giới này."*
* **AI đã giúp được gì:**
  * Cung cấp kịch bản tấn công thử nghiệm (Adversarial test) giả lập tài xế nài nỉ và ra lệnh bỏ qua bước nháp.
* **Điểm AI làm sai / Vấn đề phát sinh:**
  * Khi kiểm thử, AI đôi khi vẫn sinh thêm văn bản an ủi dài dòng trước thẻ `[DRAFT_ONLY]`, làm vi phạm quy tắc "phải xuất hiện ở ngay dòng đầu tiên".
  * *Tôi đã chỉnh sửa:* Sửa lại System Prompt với cấu trúc câu mệnh lệnh ngắn gọn, dứt khoát, bổ sung chỉ thị chống jailbreak/prompt injection và đặt `temperature=0.0` để triệt tiêu tính ngẫu nhiên của mô hình.

---

### 📌 Lần 3: Khắc phục sự cố kỹ thuật về Model và Timeout SDK
* **Vấn đề thực tế gặp phải:**
  * Mẫu ban đầu của đề bài yêu cầu gọi model `gemini-2.5-flash` và `gemini-2.0-flash`. Khi chạy thực tế, Google trả về lỗi `404 Not Found` (do các model này đã dừng cấp mới cho tài khoản mới). Tiếp tục thử `gemini-3.8-flash` thì gặp lỗi `503 Service Unavailable` do quá tải mạng.
  * Ngoài ra, autograder giới hạn thời gian chạy không quá 30 giây (`timeout=30`), nếu gọi API chậm sẽ bị đánh rớt điểm.
* **Cách tôi xử lý:**
  * Không ỷ lại vào cấu hình mẫu, tôi tự viết script liệt kê danh sách các model khả dụng (`client.models.list()`).
  * Chọn model **`gemini-3.1-flash-lite`**: Tốc độ xử lý cực nhanh (~1.5 giây/lượt), hỗ trợ đầy đủ `system_instruction` và kiểm soát ranh giới chuẩn xác.
  * Tối ưu mã nguồn: Tái sử dụng đối tượng `genai.Client` và thêm tham số `max_output_tokens=200` để AI trả lời đúng trọng tâm, rút ngắn tổng thời gian thực thi xuống ~19 giây, vượt qua bài kiểm tra của Autograder an toàn.

---

## 🔍 3. Tự đánh giá & Đúc kết kinh nghiệm

| Tiêu chí | Nhận xét thực tế cá nhân |
|---|---|
| **Mức độ phụ thuộc vào AI** | **Rất thấp:** Chỉ dùng AI để gợi ý từ khóa và kiểm tra cú pháp thư viện mới. Logic bài toán và mã nguồn chính đều do bản thân chủ động rà soát. |
| **Nhận diện lỗi của AI (Critical Thinking)** | Phát hiện được xu hướng "nịnh người dùng" của AI (dễ bị dụ bỏ qua thẻ an toàn nếu người dùng giả vờ gặp chuyện gấp) và xu hướng dùng model cũ đã bị deprecate. |
| **Giá trị rút ra lớn nhất** | Trong các bài toán AI cho doanh nghiệp lớn như Vingroup, **an toàn vận hành (Safety & Guardrails)** quan trọng hơn nhiều so với việc tạo ra một mô hình "nói nhiều". Càng cho AI quyền tự động hóa cao thì rủi ro càng lớn; luôn cần cơ chế fallback và con người kiểm duyệt (HITL). |

---

## 📌 4. Cam kết cá nhân
Tôi cam kết bản ghi chép này phản ánh đúng và trung thực quá trình học tập, tư duy phản biện và thử nghiệm kỹ thuật của bản thân trong buổi Lab 02.

