# 🔍 Phase 1 & 2: SCAN & QUICK-ASSESS (Báo cáo cá nhân)

* **Học viên thực hiện:** Vũ Xuân Hiếu
* **Nhánh Git (Branch):** `vuxuanhieu`
* **Vị trí đảm nhiệm:** AI Product Engineer — **Vin Smart Future (Vingroup)**
* **Mục tiêu:** Quét tìm các "điểm đau" (pain points) và điểm nghẽn vận hành (bottlenecks) thực tế trong hệ sinh thái Vingroup, sử dụng 4 Lăng kính (4 Lenses) và thiết lập 3 Thẻ bài toán nhanh (Quick Problem Cards).

---

## 🏛️ Bối cảnh nhiệm vụ
Tại đơn vị công nghệ hợp nhất **Vin Smart Future**, tôi tiến hành khảo sát và đánh giá thực tế hoạt động vận hành tại các công ty thành viên: **Xanh SM (GSM), VinFast, Vinhomes, Vinmec và Vinpearl**. Mục tiêu là tìm ra các quy trình nghiệp vụ thủ công đang tiêu tốn nhiều thời gian, tiềm ẩn sai sót và gây rò rỉ hiệu suất để xem xét khả năng ứng dụng AI.

---

# 🔍 Phase 1 — SCAN: Quét tìm 5 bài toán vận hành

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác) để ghi nhận 5 bài toán:

| # | Công ty thành viên | Lăng kính (Lens) | Tên bài toán & Mô tả nghiệp vụ | Ước tính tổn thất / Thời gian |
|---|--------------------|------------------|--------------------------------|-------------------------------|
| **1** | **Xanh SM (GSM)** | **Tốn thời gian** | **Xử lý sự cố cạn pin thực địa & điều phối cứu hộ sạc:**<br>Tài xế taxi điện gọi về tổng đài báo sắp hết pin hoặc cạn pin giữa đường. Điều phối viên phải tra cứu thủ công GPS của xe, kiểm tra tình trạng trụ trống của các trạm sạc VinFast xung quanh, tự gõ tin nhắn SMS chỉ dẫn hoặc gọi xe sạc pin lưu động. | ⏱ 15 - 20 phút/sự cố.<br>Tắc nghẽn giờ cao điểm, rò rỉ ~15% doanh thu cuốc xe do tài xế phải dừng hoạt động chờ cứu hộ. |
| **2** | **VinFast** | **Lặp lại** | **Đối chiếu hóa đơn tiêu thụ điện trạm sạc đối tác:**<br>Hàng tuần, bộ phận kế toán - vận hành phải so khớp thủ công hàng chục nghìn dòng log sạc xe điện từ các đơn vị đối tác liên kết bên ngoài với hóa đơn thanh toán thực tế để phát hiện chênh lệch chỉ số kWh. | ⏱ 20 giờ làm việc/tuần của đội ngũ back-office.<br>Dễ sai sót thủ công khi nhập liệu bảng tính Excel. |
| **3** | **Vinhomes** | **AI-upgrade** | **Phân loại & điều hướng phản ánh cư dân (App Resident):**<br>Cư dân gửi khiếu nại bằng văn bản tự do (tiếng ồn, hỏng thang máy, thấm dột...). Nhân viên CSKH đọc và phân loại bằng tay để chuyển tiếp cho ban quản lý từng tòa, phản hồi thường mang tính rập khuôn và chậm trễ. | ⏱ 8 - 12 tiếng để cư dân nhận được phản hồi ban đầu.<br>Tăng tỉ lệ phàn nàn và giảm chỉ số CSAT của khu đô thị. |
| **4** | **Vinmec** | **Pain từ người khác** | **Soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary):**<br>Bác sĩ điều trị phải đọc lại toàn bộ ghi chú lâm sàng, kết quả xét nghiệm, lịch sử dùng thuốc trong hệ thống HIS để tự gõ bản tóm tắt xuất viện bằng ngôn ngữ dễ hiểu cho bệnh nhân. | ⏱ 20 - 30 phút/bệnh nhân.<br>Bác sĩ phàn nàn vì kiệt sức hành chính, giảm thời gian khám chữa bệnh chuyên môn. |
| **5** | **Vinpearl** | **Tốn thời gian** | **Xử lý email đặt phòng khách sạn theo đoàn (Group Booking):**<br>Nhân viên sales/đặt phòng phải đọc các chuỗi email yêu cầu báo giá đoàn phức tạp từ các công ty lữ hành (nhiều loại phòng, ngày check-in/out lệch nhau), tự tra cứu tồn kho phòng và gõ email phản hồi. | ⏱ 25 - 40 phút/yêu cầu.<br>Tỉ lệ chốt booking bị chậm trễ so với các đối thủ cạnh tranh. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ bài toán nhanh (Quick Problem Cards)

Từ 5 bài toán trên, tôi chọn lọc ra **Top 3 bài toán tiêu biểu nhất** để phân tích sâu theo định dạng thẻ:

---

### 📇 QUICK PROBLEM CARD #1 (Ưu tiên số 1)

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Tài xế taxi điện Xanh SM báo sự cố cạn pin giữa đường cần điều phối   │
│ trạm sạc gần nhất hoặc xe sạc cứu hộ khẩn cấp.                                         │
│                                                                                        │
│ Công ty thành viên: [x] Xanh SM (GSM)     [ ] VinFast     [ ] Vinhomes                 │
│                     [ ] Vinmec            [ ] Khác (Ghi rõ): _________                 │
│                                                                                        │
│ Ai đang đau (Actor)?                                                                   │
│ - Tài xế Xanh SM: Đang hoang mang, xe sắp hết điện giữa đường phố đông đúc.             │
│ - Điều phối viên (Dispatcher): Bị quá tải tra cứu nhiều màn hình cùng lúc.              │
│                                                                                        │
│ Workflow thủ công hiện tại (5 bước):                                                   │
│   1. Nhận cuộc gọi/tin nhắn báo sự cố từ tài xế                                        │
│   ──> 2. Mở bản đồ nội bộ tra cứu tọa độ GPS thực tế của xe                            │
│   ──> 3. Mở cổng thông tin trạm sạc VinFast tìm trạm còn trụ sạc trống phù hợp         │
│   ──> 4. Soạn tin nhắn hướng dẫn đường đi chi tiết gửi qua App cho tài xế              │
│   ──> 5. Điều động xe sạc cứu hộ lưu động nếu pin xe đã cạn dưới 5%                    │
│                                                                                        │
│ Bước nào tốn thời gian / dễ lỗi nhất?                                                  │
│   Bước 3 và 4 (Tra cứu trụ sạc trống và soạn tin nhắn hướng dẫn: ⏱ 10 - 12 phút/lượt) │
│                                                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                                  │
│   Bước 3, 4 & 5: Tự động tổng hợp dữ liệu GPS + API trạm sạc -> LLM draft sẵn tin      │
│   nhắn hướng dẫn kèm cảnh báo an toàn; tự động đề xuất lệnh điều xe sạc cứu hộ nếu     │
│   mức pin < 5%.                                                                        │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   - Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút/lượt.                        │
│   - Đảm bảo 100% trường hợp pin < 5% được cảnh báo và kích hoạt xe cứu hộ kịp thời.   │
│                                                                                        │
│ Quick Architecture: [ ] No AI    [ ] Rule    [x] LLM Feature    [ ] Autonomous Agent   │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #2 (Vinhomes - Lựa chọn của nhóm)

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Điều phối viên phải xác minh loại lỗi, tra cứu lịch sử sửa chữa và   │
│ liên hệ nhân viên kỹ thuật thủ công, kéo dài thời gian phản hồi và tăng nguy cơ phân   │
│ công sai chuyên môn.                                                                   │
│                                                                                        │
│ Công ty thành viên: [ ] Xanh SM (GSM)     [ ] VinFast     [x] Vinhomes                 │
│                     [ ] Vinmec            [ ] Khác (Ghi rõ): _________                 │
│                                                                                        │
│ Ai đang đau (Actor)?                                                                   │
│   Điều phối viên bảo trì, trưởng nhóm kỹ thuật và kỹ thuật viên tòa nhà.               │
│                                                                                        │
│ Workflow thủ công hiện tại (4 bước):                                                   │
│   1. Tiếp nhận yêu cầu sửa chữa từ cư dân hoặc hệ thống quản lý.                       │
│   ──> 2. Đọc mô tả lỗi, xác minh thiết bị và tra cứu lịch sử sửa chữa.                 │
│   ──> 3. Kiểm tra lịch làm việc, chuyên môn và phân công kỹ thuật viên.                │
│   ──> 4. Kỹ thuật viên kiểm tra hiện trường, sửa chữa và cập nhật kết quả.             │
│                                                                                        │
│ Bước nào tốn thời gian / dễ lỗi nhất?                                                  │
│   Bước 2–3: Xác định lỗi và lựa chọn kỹ thuật viên (⏱ 12 phút/lượt)                     │
│                                                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                                  │
│   LLM phân tích mô tả lỗi; RAG truy xuất lịch sử bảo trì; Agent đề xuất kỹ thuật viên │
│   phù hợp theo chuyên môn, vị trí, lịch rảnh và mức độ ưu tiên. Điều phối viên phê     │
│   duyệt trước khi giao việc (HITL).                                                    │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   Thời gian điều phối dư thừa: 12 → ≤ 3 phút/yêu cầu                                   │
│                                                                                        │
│ Quick Architecture: [ ] No AI    [x] Rule    [x] LLM    [x] Agent                      │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #3 (Ưu tiên số 3)

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                                  │
│                                                                                        │
│ Bài toán (1 câu): Đối chiếu số liệu điện năng tiêu thụ hàng tuần giữa hệ thống đo trạm │
│ sạc VinFast và báo cáo hóa đơn đối tác bên ngoài để phát hiện sai lệch.                │
│                                                                                        │
│ Công ty thành viên: [ ] Xanh SM (GSM)     [x] VinFast     [ ] Vinhomes                 │
│                     [ ] Vinmec            [ ] Khác (Ghi rõ): _________                 │
│                                                                                        │
│ Ai đang đau (Actor)?                                                                   │
│ - Chuyên viên đối soát tài chính VinFast: Quá tải vì phải dò hàng vạn dòng bảng tính. │
│                                                                                        │
│ Workflow thủ công hiện tại (4 bước):                                                   │
│   1. Xuất file CSV nhật ký sạc từ trạm VinFast                                        │
│   ──> 2. Tải bảng kê hóa đơn điện từ đối tác điện lực / trung tâm thương mại           │
│   ──> 3. Dùng hàm VLOOKUP/Excel dò tìm chênh lệch kWh và mã trụ sạc                    │
│   ──> 4. Soạn email giải trình các trường hợp lệch chỉ số gửi cấp trên phê duyệt       │
│                                                                                        │
│ Bước nào tốn thời gian / dễ lỗi nhất?                                                  │
│   Bước 3 (Dò tìm sai lệch thủ công giữa các bảng dữ liệu khổng lồ: ⏱ 3 - 4 giờ/kỳ)     │
│                                                                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                                  │
│   Bước 3 và 4: Script đối chiếu tự động, LLM hỗ trợ tóm tắt nguyên nhân bất thường    │
│   (Anomalies) và draft sẵn báo cáo đối soát.                                           │
│                                                                                        │
│ Đo thành công bằng gì (Metric có số)?                                                  │
│   - Rút ngắn thời gian đối soát hàng tuần từ 20 giờ ──> dưới 30 phút.                  │
│   - Phát hiện 100% các khoản thanh toán sai lệch trên 1.000.000 VNĐ.                   │
│                                                                                        │
│ Quick Architecture: [ ] No AI    [x] Rule / Script + LLM Summary    [ ] Autonomous Agent│
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🥊 Phản biện Stress-Test từ AI (Góc nhìn CFO & Trưởng phòng Vận hành)
* **Với Card #1 (Xanh SM - Sự cố sạc pin):** Cần lưu ý việc tích hợp dữ liệu trạng thái trạm sạc thời gian thực (API Real-time) để tránh AI gợi ý trạm đang hỏng/kín chỗ. Bắt buộc có Rule chặn pin < 5% và cơ chế Human-in-the-loop (điều phối viên duyệt).
* **Với Card #2 (Vinhomes - Phân loại ticket cư dân):** Tiềm ẩn rủi ro khiếu nại nếu AI phân loại sai các sự cố khẩn cấp (rò rỉ gas, chập điện). Cần bổ sung rule-based keyword filter trước khi cho LLM xử lý.
* **Với Card #3 (VinFast - Đối chiếu hóa đơn sạc điện):** Đây là bài toán dữ liệu cấu trúc cố định. Giải pháp tối ưu chi phí và độ chính xác 100% là dùng script Python (Pandas/SQL), không nên lãng phí chi phí gọi LLM.

---

## 🎯 Kết luận lựa chọn cho bài toán Deep-Dive (Chuyển sang Phase 3)
* **Bài toán được lựa chọn của nhóm:** **Card #2 — Vinhomes: Điều phối bảo trì và phân công kỹ thuật viên thông minh**.
* **Lý do lựa chọn:**
  1. **Tính cấp thiết & Tác động vận hành lớn:** Thời gian xác minh lỗi và phân công thủ công chiếm tới 12 phút/lượt, gây tắc nghẽn nghiêm trọng cho ban quản lý tòa nhà và kéo dài thời gian chờ đợi của cư dân.
  2. **Mức độ phù hợp công nghệ (AI-Fit):** Kết hợp hoàn hảo giữa **Rule** (lọc lịch rảnh, vị trí tầng), **LLM** (đọc hiểu mô tả lỗi tiếng Việt tự do), **RAG** (truy xuất lịch sử sửa chữa thiết bị tương tự), và **Agent / Co-pilot** (tự động đề xuất kỹ thuật viên tối ưu theo chuyên môn).
  3. **Ranh giới vận hành rõ ràng:** Bắt buộc có Human-in-the-loop (Điều phối viên kiểm tra và click phê duyệt lệnh phân công trước khi giao việc cho kỹ thuật viên).
* **Lý do loại bỏ các thẻ khác:**
  * *Card #1 (Xanh SM):* Dù là bài toán hay nhưng nhóm nhận thấy quy trình bảo trì tòa nhà Vinhomes có tính đa dạng thiết bị và nhu cầu tối ưu hóa nguồn lực nhân sự kỹ thuật viên cấp bách hơn trong bối cảnh các đại đô thị Vinhomes mở rộng.
  * *Card #3 (VinFast):* Bài toán đối soát hóa đơn tài chính thuần túy phù hợp với rule-based script/ERP hơn là cần đến AI Agent.

