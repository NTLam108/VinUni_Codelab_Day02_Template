# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

| Bước | Hoạt động | Người thực hiện | Thời gian |
|---|---|---|---|
| 1 | Cư dân gửi phản ánh qua ứng dụng hoặc hotline, kèm nội dung, vị trí và hình ảnh (nếu có). | Cư dân | 2 phút |
| 2 🔄 | CSKH tiếp nhận, kiểm tra thông tin căn hộ và ghi nhận ticket vào hệ thống. | Nhân viên CSKH | 3 phút |
| 3 🔴 | Đọc nội dung, phân loại sự cố (điện, nước, vệ sinh, an ninh...), xác định mức độ ưu tiên. | Nhân viên CSKH | 6 phút |
| 4 🔴 🔄 | Tra cứu bộ phận phụ trách, đối chiếu SLA và chuyển ticket đến đơn vị xử lý. | Nhân viên CSKH | 4 phút |
| 5 | Bộ phận xử lý kiểm tra và xác nhận tiếp nhận ticket. | Bộ phận chuyên trách | 2 phút |
| **Tổng cộng** | | | **17 phút/lượt** |

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH Vinhomes và Ban Quản lý tòa nhà/khu đô thị, chịu trách nhiệm tiếp nhận, phân loại và điều phối phản ánh cư dân. |
| **2. Current Workflow** | Cư dân gửi phản ánh qua ứng dụng/hotline → CSKH tiếp nhận ticket → đọc và phân loại nội dung → tra cứu bộ phận phụ trách và SLA → chuyển ticket cho bộ phận xử lý. |
| **3. Bottleneck** | Bước đọc hiểu, phân loại và định tuyến mất khoảng **10 phút/lượt** (giả định). Dễ xảy ra sai sót khi nội dung mơ hồ, thiếu thông tin hoặc chứa nhiều vấn đề. |
| **4. Business Impact** | Giả định 25.200 ticket/tháng, riêng bước phân loại và định tuyến tiêu tốn khoảng **4.200 giờ công/tháng**, tương đương **336 triệu đồng/tháng** theo chi phí nhân sự quy đổi 80.000 đồng/giờ. Đây là chi phí thời gian ước tính, chưa phải tổn thất thực tế được xác minh. |
| **5. Success Metric** | ≥ 85% ticket được AI phân loại và đề xuất định tuyến trong ≤ 10 giây; Routing Accuracy ≥ 95%; giảm ≥ 30% thời gian xử lý trung bình tại bottleneck khi có nhân viên kiểm duyệt. |
| **6. Operational Boundary** | AI chỉ được phân tích, trích xuất thông tin, phân loại, đề xuất mức ưu tiên và bộ phận xử lý. **Không được tự ý đóng ticket, gửi phản hồi chính thức, thay đổi SLA hoặc ra quyết định đối với sự cố khẩn cấp.** Các trường hợp thiếu thông tin, mơ hồ hoặc rủi ro cao cần nhân viên xác nhận. |

### Metrics đánh giá PoC

| Metric | Baseline giả định | Target |
|---|---|---|
| Thời gian phân loại & định tuyến | 10 phút/ticket | Giảm ≥ 30% |
| Thời gian AI tạo đề xuất | Chưa có | ≤ 10 giây với ≥ 85% ticket |
| Routing Accuracy | Chưa đo | ≥ 95% |
| Tỷ lệ ticket phải chuyển lại | Chưa đo | Giảm ≥ 30% so với baseline |
| Tỷ lệ sự cố khẩn cấp được chuyển cho người kiểm tra | Chưa đo | 100% |

**Cách đo:** Routing Accuracy được tính bằng tỷ lệ đề xuất bộ phận xử lý trùng với nhãn đúng đã được chuyên viên nghiệp vụ xác nhận.

---


## 3.3. Future-State Flow & AI Fit (25 min)
**Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.

- [x] **Rule / State-Machine:** Kiểm tra dữ liệu bắt buộc, áp dụng quy tắc định tuyến và SLA.
- [x] **LLM Feature:** Đọc hiểu, phân loại nội dung tiếng Việt và trích xuất thông tin sự cố.
- [ ] **Agentic Loop:** Chưa cần cho PoC vì quy trình có thể triển khai theo luồng cố định, không cần AI tự lập kế hoạch và thực hiện nhiều hành động.


**Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

**Quy trình đề xuất:**

1. **Cư dân gửi phản ánh**
   - Nội dung phản ánh được ghi nhận vào hệ thống ticket.

2. **Rule Engine kiểm tra đầu vào**
   - Kiểm tra mã căn hộ, vị trí và thông tin bắt buộc.
   - Nhận diện các từ khóa hoặc điều kiện cần xử lý khẩn cấp.

3. **🔵 AI Step — LLM phân tích phản ánh**
   - Phân loại sự cố.
   - Trích xuất vị trí, nội dung chính và thông tin còn thiếu.
   - Đề xuất mức độ ưu tiên và nhóm xử lý.

4. **Rule Engine kiểm tra kết quả AI**
   - Đối chiếu danh mục sự cố và bộ phận phụ trách.
   - Kiểm tra SLA và điều kiện định tuyến tự động.
   - Xác định các trường hợp cần nhân viên kiểm duyệt.

5. **🟢 Human Step (HITL)**
   - CSKH kiểm tra các ticket mơ hồ, thiếu thông tin hoặc có rủi ro cao.
   - Ticket thông thường đủ điều kiện có thể được định tuyến theo các quy tắc đã phê duyệt.

6. **🔄 Chuyển ticket đến bộ phận xử lý**
   - Hệ thống ghi nhận bộ phận nhận, thời gian điều phối và lịch sử xử lý.

### ↩️ Fallback — Xử lý khi AI gặp lỗi

| Tình huống | Phương án dự phòng |
|---|---|
| LLM timeout hoặc lỗi API | Chuyển sang quy trình phân loại thủ công, không làm mất ticket. |
| Thiếu thông tin hoặc nội dung mơ hồ | Chuyển cho CSKH xác minh hoặc yêu cầu cư dân bổ sung thông tin. |
| Kết quả AI không khớp danh mục/rule | Không tự động định tuyến, chuyển nhân viên kiểm tra. |
| Phát hiện dấu hiệu sự cố khẩn cấp | Kích hoạt quy trình cảnh báo khẩn cấp hiện hành, không chờ AI tự quyết định. |

**Giá trị kỳ vọng:**
- Giảm thời gian phân loại và điều phối thủ công.
- Giảm tỷ lệ chuyển ticket sai bộ phận.
- Chuẩn hóa quy trình tiếp nhận phản ánh.
- Cải thiện khả năng đáp ứng SLA.
- Giúp CSKH tập trung vào các trường hợp phức tạp.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?

**Đánh giá:**
- AI chỉ đề xuất, không tự quyết định các trường hợp rủi ro cao.
- Rule Engine kiểm tra đầu ra của LLM.
- Nhân viên duyệt các ticket bất thường.
- Khi AI lỗi, hệ thống quay về quy trình thủ công.

Các cơ chế kiểm soát cần được kiểm chứng bằng thử nghiệm trước khi triển khai thật.

3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[x] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> Ý tưởng phân loại và định tuyến phản ánh cư dân có tiềm năng ứng dụng AI vì đầu vào chủ yếu là ngôn ngữ tự nhiên, không có cấu trúc cố định và cần hiểu ngữ cảnh để xác định đúng loại sự cố.nRule-based phù hợp với các quy tắc định tuyến rõ ràng nhưng khó bao phủ toàn bộ cách diễn đạt đa dạng của cư dân. Vì vậy, kết hợp **LLM để phân loại nội dung** và **Rule Engine để kiểm soát định tuyến** là phương án đáng thử nghiệm. Tuy nhiên, các số liệu như 10 phút/ticket, 25.200 ticket/tháng và chi phí 336 triệu đồng/tháng hiện mới là giả định. Nhóm chưa xác nhận dữ liệu ticket thực tế, baseline hiệu suất và mức độ tự động hóa hiện có của Vinhomes. Sự sẵn sàng của các bên vận hành cũng chưa được kiểm chứng. Do đó, nhóm lựa chọn **NOT YET đối với quyết định đầu tư triển khai**, nhưng có thể thực hiện một PoC offline giới hạn để kiểm chứng tính khả thi.




