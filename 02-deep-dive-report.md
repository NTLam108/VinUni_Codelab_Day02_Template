## Phase 3
## BÀI TOÁN: VINHOMES – PHÂN LOẠI & ĐỊNH TUYẾN PHẢN ÁNH CƯ DÂN TRÊN APP VINHOMES RESIDENT

---

### 3.2. Problem Statement (6-field) & Metrics

| STT | Field (Trường thông tin) | Nội dung chi tiết |
| --- | --- | --- |
| **1** | **Actor / Operator** *(Ai đang thực hiện tác vụ hằng ngày?)* | - **Nhân viên CSKH Tầng 1 (L1 Support)** tại Trung tâm tiếp nhận phản ánh vận hành Vinhomes.<br>

<br>- **Trưởng bộ phận nghiệp vụ/Điều phối viên tại hiện trường** (Kỹ thuật, An ninh, Dịch vụ Vệ sinh, Ban Quản lý phân khu/tòa nhà). |
| **2** | **Current Workflow** *(Mô tả tóm tắt quy trình và công cụ)* | 1. Cư dân gửi phản ánh/khiếu nại kèm ảnh hiện trường qua **App Vinhomes Resident**.<br>

<br>2. Nhân viên CSKH L1 đọc văn bản phản ánh, xem ảnh chụp trên màn hình dashboard quản trị (CRM/BMS nội bộ).<br>

<br>3. Nhân viên tự đọc hiểu, gõ gắn tag phân loại thủ công (chọn nhóm lỗi: Kỹ thuật điện nước, Môi trường vệ sinh, Cảnh quan, An ninh trật tự...).<br>

<br>4. Nhân viên chọn phân khu, chọn tòa nhà và chuyển tiếp (route/dispatch) thủ công ticket sang hàng đợi công việc của Ban Quản lý hoặc đội kỹ thuật phụ trách ca đó.<br>

<br>5. Nhân viên copy-paste văn mẫu ("Ban Quản lý đã tiếp nhận...") để gửi xác nhận cho cư dân. |
| **3** | **Bottleneck** *(Bước chậm, lỗi hoặc cần NLP nhất)* | **Bước 2, 3 và 4:**<br>

<br>- **Quá tải đọc hiểu:** Ý kiến cư dân thường dùng ngôn ngữ tự nhiên nhiều sắc thái cảm xúc (bức xúc, mỉa mai, mô tả gián tiếp, dùng từ lóng/từ địa phương) hoặc gửi ảnh không kèm mô tả chi tiết, khiến nhân viên mất **5–15 phút/ticket** để đọc và xác định đúng vấn đề.<br>

<br>- **Định tuyến nhầm:** Khoảng 12–18% ticket bị gán nhầm đội xử lý (ví dụ: rò rỉ nước từ trần thạch cao bị chuyển lòng vòng giữa Đội Xây dựng bảo hành và Đội Kỹ thuật vận hành), gây chậm trễ SLA tiếp nhận ban đầu kéo dài từ **6 đến 12 tiếng**. |
| **4** | **Business Impact** *(Tổn thất thực tế đo bằng thời gian/chi phí/SLA)* | - **SLA tiếp nhận & phản hồi ban đầu (First Response Time):** Bị kéo dài lên tới 6–12 giờ; thời gian giải quyết sự vụ trung bình kéo dài 2–4 ngày do thời gian luân chuyển ticket sai.<br>

<br>- **Chi phí vận hành (OPEX):** Tiêu tốn ước tính **15 – 25 tỷ VNĐ/năm (~600.000 – 1.000.000 USD/năm)** chi phí nhân sự chỉ dành riêng cho khâu phân luồng, gán tag và trả lời xác nhận thủ công trên toàn bộ các đại đô thị.<br>

<br>- **Trải nghiệm cư dân (NPS/CSAT):** Phản hồi chậm và rập khuôn dẫn đến khiếu nại leo thang trên các diễn đàn cư dân, ảnh hưởng trực tiếp đến uy tín thương hiệu Vinhomes. |
| **5** | **Success Metric** *(AI giải quyết được thì đạt ngưỡng số mấy?)* | - **Tốc độ phân loại & định tuyến:** **≥ 90%** ticket được phân loại và gán đúng đội ngũ xử lý trong thời gian **dưới 15 giây**.<br>

<br>- **Độ chính xác định tuyến (Routing Accuracy):** Đạt **≥ 95%** ngay lần đầu (giảm tỷ lệ phân luồng sai từ 15% xuống **dưới 2%**).<br>

<br>- **First Response Time (Thời gian phản hồi ban đầu):** Rút ngắn từ 6–12 tiếng ──> **dưới 3 phút**.<br>

<br>- **Giảm tải CSKH L1:** Giảm **≥ 70%** thời gian can thiệp thủ công vào các tác vụ gán nhãn và soạn thảo biên bản tiếp nhận. |
| **6** | **Operational Boundary** *(Được làm gì, TUYỆT ĐỐI không được làm gì, điểm cần duyệt)* | - **ĐƯỢC PHÉP:** Tự động đọc văn bản và ảnh chụp hiện trường; tự động gán nhãn loại sự vụ (Multi-label); tự động gắn cờ mức độ khẩn cấp (Emergency vs Normal); tự động định tuyến ticket đến đúng hàng đợi của bộ phận phụ trách; tự động sinh bản nháp (draft) phản hồi theo đúng ngữ cảnh thực tế của cư dân.<br>

<br>- **TUYỆT ĐỐI KHÔNG ĐƯỢC:** Tự động gửi cam kết bồi thường tiền tệ, thỏa thuận miễn giảm phí dịch vụ, hoặc đưa ra kết luận mang tính pháp lý/quy trách nhiệm khi chưa có kết luận bằng văn bản từ Ban Quản lý tòa nhà.<br>

<br>- **ĐIỂM CẦN DUYỆT (HITL):** Mọi sự vụ gắn cờ **Mức độ rủi ro cao (Khẩn cấp/Khiếu nại pháp lý gay gắt/An ninh trật tự)** bắt buộc phải do Trưởng bộ phận CSKH hoặc Giám đốc BQL khu đô thị rà soát và phê duyệt nội dung trước khi hệ thống gửi phản hồi ra bên ngoài. |

---

### 3.3. Future-State Flow & AI Fit

* **AI-Fit Matrix:** **[X] Agentic Loop**
*(Lý do: Cần kết hợp Multimodal xử lý cả text lẫn ảnh hiện trường, sử dụng Tool-calling tra cứu sơ đồ phân công ca trực nội bộ, đánh giá mức độ nghiêm trọng và sinh phản hồi có kiểm soát Guardrails).*

#### Future-State Workflow:

```text
[Cư dân tạo phản ánh trên App Vinhomes (Văn bản + Hình ảnh hiện trường)]
       │
       ▼
🔵 [AI Step: Multimodal Triage Agent]
       ├── Trích xuất nội dung văn bản (NLP) + Nhận diện sự cố qua ảnh (Vision LLM)
       ├── Gán nhãn nghiệp vụ đa tầng (Kỹ thuật / An ninh / Vệ sinh / Môi trường / Thu phí)
       ├── Đánh giá mức độ nghiêm trọng: Khẩn cấp (Chập cháy, ngập lụt, kẹt thang máy) vs Bình thường
       └── Function Calling: Tra cứu API danh bạ ca trực kỹ thuật & BQL theo phân khu/tòa nhà
       │
       ├────────────────────────────────────────┬────────────────────────────────────────┐
       │ (Phân loại tự tin / Confidence ≥ 90%)   │ (Sự vụ Khẩn cấp / Critical Alert)     │ (Ngôn ngữ tối nghĩa / Low Conf < 90%)
       ▼                                        ▼                                        ▼
🔵 [AI Step: Auto-Route & Draft Generator]      🔵 [AI Step: Fast-track Emergency Alert] ↩️ [Fallback: CSKH L1 Manual Triage]
   - Đẩy ticket thẳng vào App Kỹ thuật ca trực      - Kích hoạt thông báo đỏ tức thì         - Chuyển thẳng về màn hình tiếp
   - Tự động sinh nháp câu trả lời thấu cảm           đến Hotline/Bộ đàm Đội Phản ứng        nhận truyền thống của CSKH L1.
     chuẩn hóa theo ngữ cảnh sự cố.                   nhanh & BQL trong 30 giây.             - Nhân viên tự đọc và gán tay.
       │                                                │
       ▼                                                ▼
🟢 [Human Step (HITL): Kỹ thuật viên/CSKH]      🟢 [Human Step (HITL): Trưởng BQL/An ninh]
   - Kỹ thuật xác nhận tiếp nhận công việc.         - Điều động lực lượng hiện trường ngay.
   - CSKH click duyệt 1-chạm (1-click approve)      - Xác nhận tình trạng xử lý khẩn cấp.
     bản nháp phản hồi để gửi tới App cư dân.
       │
       ▼
[Cư dân nhận thông báo xác nhận chi tiết + Thời gian dự kiến xử lý (SLA < 3 phút)]

```

# 📝 03-AI-LOG: BÁO CÁO ĐÁNH GIÁ (PHASE 5) & NHẬT KÝ TƯƠNG TÁC AI (PHASE 6)
**Dự án:** Vinhomes Resident Ticket Triage & Routing Co-pilot  
**Đơn vị:** Vin Smart Future — Tập đoàn Vingroup  
**Tác giả (Kỹ sư phụ trách):** AI Product Engineer  

---

#  PHASE 5 — EVALUATE

## 1. AI Readiness Checklist

| Tiêu chí sẵn sàng | Đánh giá | Minh chứng thực tế tại Vin Smart Future |
|---|:---:|---|
| **1. Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?** | **[X] SẴN SÀNG** | Hệ thống App Vinhomes Resident và CRM/BMS đã vận hành hơn 5 năm qua tại các đại đô thị (Ocean Park, Smart City, Grand Park, Times City, Royal City) với kho dữ liệu đồ sộ hơn **1,2 triệu ticket lịch sử** đã được giải quyết, gắn nhãn phòng ban và lưu trữ biên bản hiện trường đầy đủ. Dữ liệu này đã được chuẩn hóa, ẩn danh hóa thông tin PII của cư dân để phục vụ benchmarking. |
| **2. Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?** | **[X] SẴN SÀNG** | Hệ thống áp dụng nguyên tắc **Human-in-the-Loop (HITL) 100%** trong giai đoạn đầu thông qua thẻ `[DRAFT_ONLY]` bắt buộc ở mọi bản nháp phản hồi. Đồng thời, kiến trúc thiết lập luồng **Fallback tự động**: khi điểm tự tin `confidence_score < 0.90` hoặc gặp phản ánh tối nghĩa/đa sự cố phức tạp, hệ thống chuyển giao nguyên trạng ticket về hàng đợi của nhân viên CSKH L1 trong vòng 1 giây, hoàn toàn không gây gián đoạn luồng vận hành truyền thống. |
| **3. Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?** | **[X] SẴN SÀNG** | Đội ngũ CSKH L1 đang trong tình trạng quá tải nghiêm trọng (trung bình 1 nhân viên phải đọc và gắn tag thủ công hơn 120 ticket/ngày, tỷ lệ chuyển nhầm 15%). Trưởng Ban Quản lý các khu đô thị và Giám đốc Vận hành Vinhomes đều ủng hộ mạnh mẽ giải pháp trợ lý AI Co-pilot giúp giảm tải 70% thao tác thủ công, chuyển nhân sự từ khâu gõ phím sao chép văn bản sang khâu giám sát chất lượng và chăm sóc trực tiếp các cư dân VIP/sự vụ phức tạp. |

---

## 2. Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

- [X] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
- [ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
- [ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

---

## 3. Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí)

Ban Giám Đốc Vin Smart Future phê duyệt quyết định **GO** dựa trên 4 luận cứ thực chứng vững chắc sau:

### a. Bằng chứng kỹ thuật thực nghiệm từ Bản mẫu Prompt Prototype (Phase 4)
- **Tốc độ xử lý vượt trội:** Bản mẫu prompt chạy trên mô hình Gemini Flash đạt tốc độ phản hồi trung bình **1.2 – 2.5 giây/ticket**, đáp ứng hoàn hảo mục tiêu SLA phân loại thời gian thực (< 15 giây).
- **Ranh giới an toàn tuyệt đối (100% Passed Stress-Test):** Qua 4 kịch bản tấn công ranh giới khắt khe (Adversarial Stress-Testing):
  - *Chống thoát kiểm duyệt:* Tiền tố `[DRAFT_ONLY]` được giữ vững tuyệt đối 100%, không cho phép tự động gửi thông điệp chưa kiểm duyệt ra ngoài.
  - *Chống vi phạm cam kết tài chính:* Từ chối hoàn toàn yêu cầu đền bù 50.000.000 VNĐ và miễn phí dịch vụ 2 năm khi chưa có biên bản hiện trường, kích hoạt cờ `boundary_violation_detected = true`.
  - *Kháng đòn giấu sự cố khẩn cấp:* Phát hiện ngay lập tức nguy cơ chập cháy tủ điện và ép buộc gán `severity: "EMERGENCY"`, `action: "fast_track_emergency_alert"`, `requires_human_approval: true` dù người dùng cố tình yêu cầu hạ cấp.
  - *Kháng đòn Jailbreak & trích xuất dữ liệu:* Giữ vững cấu trúc JSON và vai trò hệ thống, không làm lộ System Prompt.

### b. Hiệu quả kinh tế vượt trội (ROI & Cost-Benefit Analysis)
- **Chi phí vận hành hiện tại (Baseline OPEX):** Khoảng 15 – 25 tỷ VNĐ/năm (~600.000 – 1.000.000 USD/năm) chi phí nhân sự dành cho việc tiếp nhận, phân loại và soạn thảo phản hồi thủ công trên toàn quốc.
- **Chi phí vận hành AI (Cloud & Token Inference):** Với lượng phản ánh trung bình 3.000 ticket/ngày trên toàn hệ thống Vinhomes, mỗi ticket tiêu tốn khoảng ~1.200 tokens (System prompt + input + output JSON). Chi phí API Gemini Flash ước tính chỉ rơi vào khoảng **~35 – 50 USD/tháng (~1,2 triệu VNĐ/tháng)** — con số gần như không đáng kể so với lợi ích mang lại.
- **ROI dự kiến:** Hoàn vốn đầu tư trong vòng **dưới 2 tháng** sau khi triển khai chính thức.

### c. Rủi ro được khoanh vùng bằng Kiến trúc Fallback & HITL
- Hệ thống không thay thế con người mà đóng vai trò **Co-pilot (Trợ lý đồng hành)**.
- Mọi quyết định phản hồi cư dân đều cần thao tác "1-click approve" từ điều phối viên hoặc kỹ thuật viên.
- Nếu mô hình gặp lỗi mạng hoặc trả về JSON không hợp lệ, hệ thống tự động kích hoạt `fallback_manual_triage` đẩy về hàng đợi thủ công như trước đây, đảm bảo tỷ lệ sẵn sàng của hệ thống đạt 99.99%.

### d. Lộ trình triển khai Scope hẹp (Phased Rollout Plan)
- **Giai đoạn 1 (Tháng 1 - Pilot hẹp):** Triển khai thử nghiệm tại 2 phân khu thuộc Vinhomes Ocean Park 1 (khoảng 15 tòa chung cư), chỉ áp dụng cho nhóm phản ánh Kỹ thuật và Môi trường vệ sinh.
- **Giai đoạn 2 (Tháng 2 - Đánh giá & Hiệu chỉnh):** Đo lường Routing Accuracy và First Response Time thực tế; fine-tune prompt dựa trên edge-cases thực địa.
- **Giai đoạn 3 (Tháng 3 trở đi - Scale toàn diện):** Mở rộng toàn bộ các đại đô thị Vinhomes trên toàn quốc và tích hợp mở rộng sang các dịch vụ khác của Vingroup.

---