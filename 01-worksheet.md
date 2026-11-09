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
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên xử lý thủ công các phản hồi khẩn cấp từ tài xế về sự cố cạn pin hoặc tìm trạm sạc thực địa (mất 15-20 min/lượt). |
| 2 | **VinFast** | Lặp lại | So khớp hóa đơn sạc điện và đối chiếu số liệu trạm sạc đối tác hằng tuần giữa dữ liệu log kWh và hóa đơn thanh toán. |
| 3 | **Vinhomes** | AI-upgrade | Hệ thống phân loại và route tự động các phản hồi/khiếu nại của cư dân trên App Vinhomes Resident đến đúng ban quản lý từng tòa nhà. |
| 4 | **Vinmec** | Pain từ người khác | Bác sĩ mất quá nhiều thời gian viết tóm tắt hồ sơ xuất viện (Discharge Summary 20-30 min/bệnh nhân), gây quá tải lâm sàng. |
| 5 | **Vinpearl** | Tốn thời gian | Đọc và xử lý email đặt phòng khách sạn theo đoàn (Group Booking) phức tạp từ các công ty lữ hành để kiểm tra phòng trống và báo giá. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

### Quick Problem Card #1:
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Tài xế taxi điện Xanh SM báo sự cố cạn pin│
│ giữa đường cần điều phối cứu hộ hoặc trạm sạc gần nhất.     │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM & Điều phối viên        │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhận báo sự cố ──> 2. Tra GPS xe ──> 3. Tìm trạm trống │
│   ──> 4. Soạn tin hướng dẫn ──> 5. Điều xe cứu hộ nếu pin<5%│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 12 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3, 4 & 5 (Auto   │
│ tổng hợp trạm sạc, draft tin nhắn, trigger cứu hộ pin < 5%) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   Giảm thời gian xử lý sự cố từ 15 min ──> under 3 min.     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #2:
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Điều phối viên phải xác minh loại lỗi, tra cứu lịch sử sửa chữa và liên hệ nhân viên kỹ thuật thủ công, kéo dài thời gian phản hồi và tăng nguy cơ phân công sai chuyên môn.  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Điều phối viên bảo trì, trưởng nhóm kỹ thuật và kỹ thuật viên tòa nhà. │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tiếp nhận yêu cầu sửa chữa từ cư dân hoặc hệ thống quản lý. ──> 2. Đọc mô tả lỗi, xác minh thiết bị và tra cứu lịch sử sửa chữa. ──> 3. Kiểm tra lịch làm việc, chuyên môn và phân công kỹ thuật viên. ──> 4. Kỹ thuật viên kiểm tra hiện trường, sửa chữa và cập nhật kết quả.                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3: xác định lỗi và lựa chọn kỹ thuật viên (⏱ 12 phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? LLM phân tích mô tả lỗi; RAG truy xuất lịch sử bảo trì; Agent đề xuất kỹ thuật viên phù hợp theo chuyên môn, vị trí, lịch rảnh và mức độ ưu tiên. Điều phối viên phê duyệt trước khi giao việc. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Thời gian điều phối dư thừa: 12 → ≤ 3 phút/yêu cầu│
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #3:
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Đối chiếu số liệu điện năng tiêu thụ hàng │
│ tuần giữa hệ thống trạm sạc VinFast và hóa đơn đối tác ngoài│
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Chuyên viên đối soát tài chính VinFast │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Xuất file log sạc ──> 2. Tải bảng hóa đơn đối tác      │
│   ──> 3. Dò VLOOKUP tìm lệch kWh ──> 4. Soạn email giải trình│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 3-4 giờ/kỳ)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 & 4 (Phát hiện │
│ bất thường và draft báo cáo đối soát tự động)               │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   Giảm thời gian đối soát tuần từ 20 giờ ──> under 30 min.  │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

### 🥊 Phản biện Stress-Test từ AI (Góc nhìn CFO & Trưởng phòng Vận hành):
1. **Với Card #1 (Xanh SM - Sự cố sạc pin):**
   * *Điểm yếu cần lưu ý:* Nếu chỉ dựa vào AI để tự động điều hướng mà không có dữ liệu trạng thái trạm sạc thời gian thực (API Real-time status), AI có thể chỉ tài xế đến trạm đang hỏng hoặc đã kín chỗ. Do đó, **bắt buộc phải có Rule kiểm tra pin < 5% và Human-in-the-loop (điều phối viên duyệt)**.
2. **Với Card #2 (Vinhomes - Phân loại ticket cư dân):**
   * *Điểm yếu:* Nguy cơ khiếu nại pháp lý hoặc mâu thuẫn cư dân nếu AI phân loại sai mức độ khẩn cấp (ví dụ: rò rỉ khí gas/chập cháy mà bị xếp vào ticket thường). Rule-based lọc từ khóa khẩn cấp vẫn an toàn hơn nếu chưa có dữ liệu gán nhãn chuẩn.
3. **Với Card #3 (VinFast - Đối chiếu hóa đơn sạc điện):**
   * *Điểm yếu:* Đây thuần túy là bài toán đối soát số liệu có cấu trúc. Sử dụng code Python (Pandas/SQL) hoặc hệ thống ERP đối chiếu theo luật (Rule-based) sẽ rẻ hơn 100 lần, nhanh hơn và chính xác 100% so với dùng LLM.

### 🗳️ Quyết định lựa chọn bài toán để làm Deep-Dive (Phase 3):
* **LỰA CHỌN CHÍNH THỨC CỦA NHÓM:** **Card #2 — Vinhomes: Điều phối bảo trì và phân công kỹ thuật viên thông minh**.
* **Lý do lựa chọn:**
  * **Tính cấp thiết & Tác động vận hành lớn:** Thời gian xác minh lỗi và phân công thủ công chiếm tới 12 phút/lượt, gây tắc nghẽn nghiêm trọng cho ban quản lý tòa nhà và kéo dài thời gian chờ đợi của cư dân.
  * **Mức độ phù hợp công nghệ (AI-Fit):** Kết hợp hoàn hảo giữa **Rule** (lọc lịch rảnh, vị trí tầng), **LLM** (đọc hiểu mô tả lỗi tiếng Việt tự do), **RAG** (truy xuất lịch sử sửa chữa thiết bị tương tự), và **Agent / Co-pilot** (tự động đề xuất kỹ thuật viên tối ưu theo chuyên môn).
  * **Ranh giới vận hành rõ ràng:** Bắt buộc có Human-in-the-loop (Điều phối viên kiểm tra và click phê duyệt lệnh phân công trước khi giao việc cho kỹ thuật viên).
* **Lý do loại bỏ các thẻ khác:**
  * *Card #1 (Xanh SM):* Dù là bài toán hay nhưng nhóm nhận thấy quy trình bảo trì tòa nhà Vinhomes có tính đa dạng thiết bị và nhu cầu tối ưu hóa nguồn lực nhân sự kỹ thuật viên cấp bách hơn trong bối cảnh các đại đô thị Vinhomes mở rộng.
  * *Card #3 (VinFast):* Bài toán đối soát hóa đơn tài chính thuần túy phù hợp với rule-based script/ERP hơn là cần đến AI Agent.

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại:** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước 2 (Đọc hiểu phân loại ticket) & Bước 3 (Tra cứu BQL tòa và gán thủ công).
* 🔄 **Handoff:** Cư dân ──> CSKH Trung tâm ──> BQL Tòa nhà ──> Đội Kỹ thuật/An ninh.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = 12 - 15 phút/lượt** (Cư dân chờ phản hồi từ 8 - 12 tiếng).

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│ Bước 1          │       │ Bước 2          │       │ Bước 3          │       │ Bước 4          │
│ Cư dân gửi text │ ──🔄──>│ CSKH đọc hiểu   │ ──🔄──>│ Tra cứu BQL tòa │ ──🔄──>│ Soạn tin nhắn   │
│ phản ánh tự do  │       │ & phân loại lỗi │       │ & gán ticket    │       │ xác nhận        │
│ ⏱ 3 phút        │       │ ⏱ 5 phút 🔴     │       │ ⏱ 5 phút 🔴     │       │ ⏱ 2 phút        │
└─────────────────┘       └─────────────────┘       └─────────────────┘       └─────────────────┘
```

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH tại Trung tâm Vận hành Vinhomes và Điều phối viên BQL tòa nhà. |
| **2. Current Workflow** | Cư dân gửi phản ánh tự do qua App Vinhomes Resident. CSKH đọc thủ công, phân loại sự cố (kỹ thuật, an ninh, vệ sinh), tra cứu căn hộ/tòa nhà, gán ticket cho bộ phận liên quan và gửi tin nhắn xác nhận. |
| **3. Bottleneck** | Bước 2 & 3: Quá tải giờ cao điểm, phân loại thủ công mất 10 phút/ticket, tỷ lệ gán nhầm phòng ban chiếm 18%. |
| **4. Business Impact** | ~30.000 ticket/tháng, tiêu tốn 5.000 giờ làm việc CSKH/tháng. Cư dân chờ 8-12 tiếng làm giảm chỉ số CSAT xuống dưới 78%. |
| **5. Success Metric** | 1. Tự động hóa phân loại ticket dưới 15 giây (85% vé được phân loại dưới 10s).<br>2. Độ chính xác phân loại bộ phận đạt $\ge 92\%$.<br>3. Thời gian phản hồi cư dân giảm từ 8 tiếng xuống dưới 2 phút. |
| **6. Operational Boundary** | AI được phép trích xuất thực thể, phân loại intent và đề xuất routing. TUYỆT ĐỐI KHÔNG tự ý đóng ticket hoặc từ chối yêu cầu. Nếu gặp từ khóa khẩn cấp (cháy nổ, kẹt thang, rò rỉ gas), lập tức còi báo động chuyển sang hotline an ninh. Bắt buộc CSKH duyệt (HITL) với các khiếu nại tài chính/pháp lý. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm: `[x] LLM Feature (kết hợp Rule-based keyword filtering)`.
* **Vẽ Future-State Flow:**
  * 🔵 **AI Step:** LLM đọc hiểu ngôn ngữ tự nhiên, phân loại intent và trích xuất thực thể (tòa nhà, số phòng, thiết bị hỏng).
  * 🟢 **Human Step (HITL):** CSKH duyệt 1-click hoặc tự động gửi nếu confidence score $\ge 90\%$.
  * ↩️ **Fallback:** Nếu LLM có độ tự tin $< 80\%$ hoặc lỗi mạng, tự động chuyển về hàng đợi thủ công cho CSKH xử lý như quy trình cũ.

```text
Cư dân gửi App ──> [Rule quét từ khóa khẩn cấp] ──> 🔵 [LLM phân loại & Route] ──> 🟢 [CSKH duyệt / Gửi BQL]
                           │ (Nếu khẩn cấp)                 │ (Confidence < 80%)
                           ▼                                ▼
                  🚨 [Báo động An ninh]            ↩️ [Fallback: CSKH gán tay]
```

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? (Hơn 100.000 ticket lịch sử tại Vinhomes)
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? (Có Rule Engine lọc từ khóa nguy hiểm và cơ chế Fallback khi confidence < 80%)
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? (BQL và CSKH rất ủng hộ để giảm tải 80% công việc thủ công)

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp (Module phân loại intent và trích xuất thực thể).
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> Dự án đạt mức độ **GO** vì:
> 1. **Hiệu quả kinh tế & vận hành:** Giảm 80% thời gian xử lý ticket của CSKH (tiết kiệm ~5.000 giờ/tháng), rút ngắn thời gian phản hồi cư dân từ 8-12 tiếng xuống dưới 2 phút, cải thiện rõ rệt chỉ số hài lòng CSAT.
> 2. **Tính khả thi kỹ thuật:** Bài toán phân loại văn bản tiếng Việt và trích xuất thực thể (NER) là thế mạnh của các mô hình LLM hiện đại (Gemini Flash). Chi phí API cực thấp (~0.0001$/ticket), ROI ước tính đạt trên 500%.
> 3. **Kiểm soát rủi ro an toàn:** Thiết lập ranh giới an toàn đa tầng với Rule Engine cảnh báo còi báo động cho trường hợp khẩn cấp, HITL duyệt cho các khiếu nại tài chính/pháp lý và Fallback về người nếu độ tin cậy thấp.

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
