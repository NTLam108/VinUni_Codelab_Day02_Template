# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |Vinhomes |Lặp lại |Nhân viên CSKH phải đọc, phân loại và chuyển phản ánh từ Vinhomes Resident đến đúng bộ phận kỹ thuật, an ninh hoặc vệ sinh. |
| 2 |Vinhomes |Tốn thời gian |Nhân viên kỹ thuật phải đọc mô tả lỗi, tra cứu lịch sử sửa chữa, kiểm tra thiết bị và phân công thợ phù hợp. |
| 3 |Vinhomes |Lặp lại |Kế toán phải xác minh các giao dịch chưa khớp giữa hệ thống thu phí, ngân hàng và thông tin căn hộ, đặc biệt khi cư dân chuyển khoản sai nội dung. |
| 4 |Vinhomes |Pain từ người khác |Ban quản lý phải tổng hợp ảnh, biên bản vệ sinh, bảo vệ, cảnh quan từ nhà thầu để kiểm tra vi phạm SLA và yêu cầu khắc phục. |
| 5 |Vinhomes |AI có thể tốt hơn |Nhân viên bàn giao phải đối chiếu checklist nghiệm thu, ảnh hiện trạng, biên bản lỗi và hồ sơ khách hàng để xác nhận các hạng mục cần sửa. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌───────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                             │
│                                                                   │
│ Bài toán (1 câu):                                                 │
│ Nhân viên CSKH phải đọc, phân loại và chuyển thủ công phản ánh cư │
│ dân đến đúng bộ phận xử lý, gây chậm trễ và nguy cơ chuyển sai    │
│ yêu cầu.                                                          │
│                                                                   │
│ Công ty thành viên:                                               │
│ [ ] VinFast [ ] Xanh SM [x] Vinhomes [ ] Vinmec                   │
│ [ ] Khác (Ghi rõ)________                                         │
│                                                                   │
│ Ai đang đau (Actor)?                                              │
│ Nhân viên CSKH và Ban Quản lý tòa nhà/khu đô thị.                 │
│                                                                   │
│ Workflow thủ công hiện tại (3-5 bước):                            │
│ 1. Cư dân gửi phản ánh qua ứng dụng cư dân hoặc hotline.          │
│ 2. CSKH đọc nội dung, xác định loại sự cố và mức độ khẩn cấp.     │
│ 3. Tra cứu bộ phận phụ trách, chuyển ticket và gán SLA.           │
│ 4. Bộ phận tiếp nhận xác nhận, xử lý và cập nhật trạng thái.      │
│                                                                   │
│ Bước nào tốn thời gian/lỗi nhất?                                  │
│ Bước 2–3: phân loại và chuyển ticket (⏱ 10 phút/lượt)             │
│                                                                   │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                             │
│ Bước 2–3: LLM phân loại nội dung tiếng Việt, trích xuất vị trí/sự │
│ cố, đề xuất mức ưu tiên; Rule Engine định tuyến đến bộ phận theo  │
│ SLA. Các trường hợp thiếu thông tin hoặc độ tin cậy thấp được     │
│ chuyển cho nhân viên xác nhận.                                    │
│                                                                   │
│ Đo thành công bằng gì (Metric có số)?                             │
│ Thời gian phân loại/điều phối: 5 → ≤ 1 phút/ticket                │
│ VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"      │
│                                                                   │
│ Quick Architecture:                                               │
│ [ ] No AI [x] Rule [x] LLM [ ] Agent                              │
└───────────────────────────────────────────────────────────────────┘
┌───────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                             │
│                                                                   │
│ Bài toán (1 câu):                                                 │
│ Điều phối viên phải xác minh loại lỗi, tra cứu lịch sử sửa chữa   │
│ và liên hệ nhân viên kỹ thuật thủ công, kéo dài thời gian phản    │
│ hồi và tăng nguy cơ phân công sai chuyên môn.                     │
│                                                                   │
│ Công ty thành viên:                                               │
│ [ ] VinFast [ ] Xanh SM [x] Vinhomes [ ] Vinmec                   │
│ [ ] Khác (Ghi rõ)________                                         │
│                                                                   │
│ Ai đang đau (Actor)?                                              │
│ Điều phối viên bảo trì, trưởng nhóm kỹ thuật và kỹ thuật viên tòa │
│ nhà.                                                              │
│                                                                   │
│ Workflow thủ công hiện tại (3-5 bước):                            │
│ 1. Tiếp nhận yêu cầu sửa chữa từ cư dân hoặc hệ thống quản lý.    │
│ 2. Đọc mô tả lỗi, xác minh thiết bị và tra cứu lịch sử sửa chữa.  │
│ 3. Kiểm tra lịch làm việc, chuyên môn và phân công kỹ thuật viên. │
│ 4. Kỹ thuật viên kiểm tra hiện trường, sửa chữa và cập nhật kết   │
│ quả.                                                              │
│                                                                   │
│ Bước nào tốn thời gian/lỗi nhất?                                  │
│ Bước 2–3: xác định lỗi và lựa chọn kỹ thuật viên (⏱ 12 phút/lượt) │
│                                                                   │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                             │
│ LLM phân tích mô tả lỗi; RAG truy xuất lịch sử bảo trì; Agent đề  │
│ xuất kỹ thuật viên phù hợp theo chuyên môn, vị trí, lịch rảnh và  │
│ mức độ ưu tiên. Điều phối viên phê duyệt trước khi giao việc.     │
│                                                                   │
│ Đo thành công bằng gì (Metric có số)?                             │
│ Thời gian điều phối dư thừa: 12 → ≤ 3 phút/yêu cầu                │
│                                                                   │
│ Quick Architecture:                                               │
│ [ ] No AI [x] Rule [x] LLM [x] Agent                              │
└───────────────────────────────────────────────────────────────────┘

┌───────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                             │
│                                                                   │
│ Bài toán (1 câu):                                                 │
│ Nhân viên kế toán phải kiểm tra và đối chiếu thủ công những khoản │
│ thanh toán thiếu hoặc sai thông tin căn hộ, gây tồn đọng giao     │
│ dịch chưa xác định và nguy cơ sai lệch công nợ.                   │
│                                                                   │
│ Công ty thành viên:                                               │
│ [ ] VinFast [ ] Xanh SM [x] Vinhomes [ ] Vinmec                   │
│ [ ] Khác (Ghi rõ)________                                         │
│                                                                   │
│ Ai đang đau (Actor)?                                              │
│ Nhân viên kế toán công nợ, bộ phận thu phí và CSKH tại Ban Quản   │
│ lý.                                                               │
│                                                                   │
│ Workflow thủ công hiện tại (3-5 bước):                            │
│ 1. Xuất dữ liệu giao dịch ngân hàng và danh sách công nợ căn hộ.  │
│ 2. Đối chiếu số tiền, thời gian, mã căn hộ và nội dung chuyển     │
│ khoản                                                             │
│ 3. Tra cứu giao dịch không khớp, liên hệ cư dân hoặc CSKH xác     │
│ minh                                                              │
│ 4. Xác nhận thanh toán và cập nhật công nợ vào hệ thống           │
│                                                                   │
│ Bước nào tốn thời gian/lỗi nhất?                                  │
│ Bước 2–3, xác minh các giao dịch ngoại lệ. (⏱ 8 phút/lượt)        │
│                                                                   │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                             │
│ Rule Engine đối chiếu chính xác các trường dữ liệu; AI Matching   │
│ chuẩn hóa nội dung chuyển khoản, nhận diện mã căn hộ viết sai và  │
│ đề xuất giao dịch tương ứng để kế toán xác nhận.                  │
│                                                                   │
│ Đo thành công bằng gì (Metric có số)?                             │
│ Thời gian xử lý ngoại lệ: 8 → ≤ 2 phút/giao dịch. Precision của   │
│ đề xuất ghép giao dịch: ≥ 90% trên các trường hợp hệ thống đề     │
│ xuất khớp.                                                        │
│ VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"      │
│                                                                   │
│ Quick Architecture:                                               │
│ [ ] No AI [x] Rule [x] LLM [ ] Agent                              │
└───────────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

