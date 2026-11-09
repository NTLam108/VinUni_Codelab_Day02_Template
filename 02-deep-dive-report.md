# 🏢 Báo Cáo Chuyên Sâu (Deep-Dive Report) — Vin Smart Future

* **Dự án:** Trợ lý AI Phân loại & Định tuyến phản ánh cư dân (Vinhomes Smart Resident Routing)
* **Đơn vị thành viên:** **Vinhomes**
* **Người thực hiện:** Vũ Xuân Hiếu (và Nhóm dự án)
* **Nhánh Git (Branch):** `vuxuanhieu`

---

## 🏛️ 1. Bối cảnh & Lý do lựa chọn bài toán

Tại các đại đô thị của **Vinhomes** (Vinhomes Ocean Park, Smart City, Grand Park...), mỗi ngày Ban Quản lý (BQL) tiếp nhận từ **800 đến 1.500 phản ánh/yêu cầu** từ cư dân thông qua App Vinhomes Resident. Các phản ánh rất đa dạng: từ sự cố kỹ thuật (thang máy, mất nước, chập điện), an ninh trật tự (đỗ xe sai quy định, tiếng ồn đêm khuya), đến vệ sinh môi trường và thủ tục hành chính.

Hiện tại, toàn bộ khâu đọc hiểu, phân loại và gán ticket cho bộ phận xử lý đều được thực hiện **thủ công**, dẫn đến tình trạng quá tải nghiêm trọng, kéo dài thời gian phản hồi cư dân từ 8 đến 12 tiếng, làm giảm chỉ số hài lòng (CSAT) của cư dân. Nhóm quyết định chọn bài toán này để thực hiện Deep-Dive nhằm số hóa và tối ưu hóa quy trình tiếp nhận dịch vụ cư dân.

---

# 🏗️ Phase 3 — DEEP-DIVE

## 3.1. Sơ đồ quy trình hiện tại (Current-State Workflow Mapping)

Quy trình tiếp nhận và xử lý phản ánh thủ công hiện tại:

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│ Bước 1          │       │ Bước 2          │       │ Bước 3          │       │ Bước 4          │
│ Cư dân gửi text │       │ CSKH đọc hiểu   │       │ Tra cứu BQL tòa │       │ Soạn tin nhắn   │
│ phản ánh tự do  │ ──🔄──>│ & phân loại lỗi │ ──🔄──>│ & gán ticket thủ│ ──🔄──>│ xác nhận gửi    │
│ trên App        │       │                 │       │ công            │       │ lại cư dân      │
│ Ai: Cư dân      │       │ Ai: CSKH        │       │ Ai: CSKH        │       │ Ai: CSKH        │
│ ⏱ 3 phút        │       │ ⏱ 5 phút 🔴     │       │ ⏱ 5 phút 🔴     │       │ ⏱ 2 phút        │
│ In: Raw text/ảnh│       │ In: Mô tả tự do │       │ In: Số căn/tòa  │       │ In: Mẫu tin     │
│ Out: Ticket thô │       │ Out: Nhãn sự cố │       │ Out: Phân công  │       │ Out: SMS/Noti   │
└─────────────────┘       └─────────────────┘       └─────────────────┘       └─────────────────┘
                                                                                      │
                                                                                      ▼
                                                                               ┌─────────────────┐
                                                                               │ Bước 5          │
                                                                               │ Đội Kỹ thuật /  │
                                                                               │ An ninh tiếp    │
                                                                               │ nhận & xử lý    │
                                                                               │ Ai: Kỹ thuật BQL│
                                                                               │ ⏱ 2 - 4 giờ     │
                                                                               └─────────────────┘
```
* 🔴 **Bottleneck (Điểm nghẽn):** Bước 2 và Bước 3 tiêu tốn trung bình **10 phút/ticket** do nhân viên phải đọc văn bản tiếng Việt tự do (có từ viết tắt, tiếng lóng, mô tả không rõ ràng) và tra cứu sơ đồ phân công từng tòa.
* 🔄 **Handoff (Điểm chuyển giao):** Chuyển giao thông tin từ Cư dân $\rightarrow$ Tổng đài CSKH $\rightarrow$ BQL tòa nhà $\rightarrow$ Kỹ thuật viên hiện trường.
* ⏱ **Tổng thời gian tiếp nhận & điều phối thủ công:** **12 - 15 phút/ticket**; thời gian cư dân nhận phản hồi ban đầu kéo dài **8 - 12 tiếng** vào giờ cao điểm.

---

## 3.2. Problem Statement (6-Field) — Chuẩn Vin Smart Future

| Trường thông tin | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên Chăm sóc khách hàng (CSKH) tại Trung tâm Vận hành Vinhomes và Điều phối viên BQL tòa nhà. |
| **2. Current Workflow** | Cư dân gửi phản ánh bằng văn bản tự do kèm hình ảnh qua App Vinhomes Resident. Nhân viên CSKH đọc thủ công, xác định loại sự cố (kỹ thuật, an ninh, vệ sinh, hành chính), tra cứu mã căn hộ/tòa nhà, gán ticket cho bộ phận liên quan và soạn thông báo xác nhận gửi lại cư dân. |
| **3. Bottleneck** | **Bước 2 & 3 (Đọc hiểu, gán nhãn và định tuyến):** Quá tải khi lượng ticket dồn vào giờ cao điểm (7h-9h sáng và 18h-21h tối). Nhân viên phân loại sai chuyên môn (ví dụ: tiếng ồn kỹ thuật thang máy bị gán nhầm sang ban an ninh) chiếm tới 18% tổng số ticket. |
| **4. Business Impact** | Mỗi tháng có ~30.000 ticket trên toàn hệ thống Vinhomes. Tốn ~5.000 giờ làm việc thủ công/tháng của đội ngũ CSKH. Thời gian cư dân chờ tiếp nhận kéo dài 8-12 tiếng làm giảm chỉ số CSAT xuống dưới 78%; tỷ lệ cư dân bức xúc gọi hotline khiếu nại tăng 25%. |
| **5. Success Metric** | 1. **Thời gian định tuyến ticket (Efficiency):** Giảm từ 10 phút xuống **dưới 15 giây/ticket** (Tự động 100%).<br>2. **Độ chính xác phân loại (Quality):** Tỉ lệ phân loại đúng phòng ban xử lý đạt **$\ge 92\%$**.<br>3. **Thời gian phản hồi cư dân:** Từ 8 tiếng giảm xuống **dưới 2 phút**. |
| **6. Operational Boundary (Ranh giới an toàn)** | **ĐƯỢC PHÉP:** Tự động phân loại danh mục, trích xuất thực thể (tòa, tầng, thiết bị) và gợi ý route cho BQL.<br>**CẤM TUYỆT ĐỐI:** AI không được tự ý đóng ticket hoặc từ chối phản ánh của cư dân. Với các sự cố khẩn cấp đe dọa tính mạng/an toàn (chập cháy, rò rỉ khí gas, kẹt thang máy), AI **PHẢI** kích hoạt đường dây nóng khẩn cấp cho ban an ninh lập tức và gửi cảnh báo trực quan cho điều phối viên. Bắt buộc có Human-in-the-loop (HITL) phê duyệt đối với các khiếu nại pháp lý, phí dịch vụ. |

---

## 3.3. Future-State Flow & AI Fit

* **Đánh giá mức độ phù hợp (AI-Fit Matrix):** **LLM Feature kết hợp Rule Engine (Hybrid Architecture)**.
  * Dùng *Rule Engine* để kiểm tra các từ khóa khẩn cấp nguy hiểm (cháy, nổ, kẹt thang) để ưu tiên số 1.
  * Dùng *LLM Classifier (Gemini Flash)* để đọc hiểu ngữ cảnh tiếng Việt tự do, trích xuất intent và phân loại chính xác danh mục nghiệp vụ.
  * Chưa cần dùng Autonomous Multi-Agent để tránh rủi ro hallucination và tối ưu chi phí vận hành.

* **Sơ đồ quy trình tương lai (Future-State Flow):**

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│ Bước 1          │       │ Bước 2 (Rule)   │       │ Bước 3 (AI Step)│       │ Bước 4 (HITL)   │
│ Cư dân gửi text │ ───>  │ Quét từ khóa    │ ───>  │ 🔵 LLM phân loại│ ───>  │ 🟢 CSKH / BQL   │
│ phản ánh trên   │       │ khẩn cấp (cháy, │       │ intent, phòng   │       │ 1-click duyệt   │
│ App Resident    │       │ kẹt thang máy)  │       │ ban & trích xuất│       │ hoặc tự động gửi│
└─────────────────┘       └─────────────────┘       └─────────────────┘       └─────────────────┘
                                   │ (Nếu khẩn cấp)          │ (Confidence < 80%)       │
                                   ▼                         ▼                          ▼
                          ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
                          │ 🚨 Còi báo động  │       │ ↩️ Fallback:    │       │ Hoàn tất trong  │
                          │ Route ngay cho  │       │ Chuyển sang hàng│       │ dưới 30 giây!   │
                          │ An ninh xử lý   │       │ đợi thủ công    │       │ Cư dân nhận SMS │
                          │ ngay lập tức!   │       │ cho CSKH gán tay│       │ xác nhận tức thì│
                          └─────────────────┘       └─────────────────┘       └─────────────────┘
```

---

# 🏁 Phase 5 — EVALUATE: Quyết định của Ban Giám Đốc Vin Smart Future

### 📋 AI Readiness Checklist:
1. **[x] Dữ liệu mẫu:** Vinhomes đã có kho dữ liệu lịch sử hơn 100.000 ticket khiếu nại đã được gán nhãn thực tế từ các năm trước.
2. **[x] Rủi ro kiểm soát được:** Có chốt chặn Rule Engine phát hiện từ khóa nguy hiểm và cơ chế Fallback (chuyển sang người duyệt nếu AI có độ tự tin < 80%).
3. **[x] Sự sẵn sàng của Stakeholders:** Ban Quản lý Vinhomes và bộ phận CSKH rất ủng hộ vì giải pháp giúp giảm 80% áp lực gõ phím và đọc ticket hàng ngày.

---

### 🗳️ Quyết định cuối cùng: **GO (Bắt đầu xây dựng Prototype)**

**Lý giải quyết định (Justification):**
1. **Lợi ích kinh tế & hiệu suất rõ ràng:** Tiết kiệm hơn **4.000 giờ làm việc/tháng** cho khối CSKH toàn hệ thống, tương đương cắt giảm chi phí vận hành ~250 triệu VNĐ/tháng.
2. **Chi phí triển khai thấp:** Sử dụng mô hình nhẹ `gemini-3.1-flash-lite` với chi phí token cực thấp (~0.0001 USD/ticket), chi phí API hàng tháng chỉ khoảng vài chục USD, ROI đạt trên 500%.
3. **Rủi ro vận hành thấp:** Luôn có con người kiểm duyệt (HITL) cho các trường hợp không chắc chắn và cơ chế còi báo động cho trường hợp khẩn cấp.

