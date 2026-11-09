# 🏗️ Phase 3 — DEEP-DIVE 
## 3.1. Current-State Workflow Mapping

```text
┌────────────────────────────────────────────────────┐
│ [1] Kiểm tra mức pin (SOC)                         │
└────────────────────────────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────┐
│ [2] Tìm kiếm trạm sạc gần vị trí hiện tại          │
│     hoặc điểm đến                                  │
│                                                    │
│     >>> BOTTLENECK (5–30 phút/lượt)                │
└────────────────────────────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────┐
│ [3] Đánh giá và lựa chọn trạm sạc                  │
│     - Khoảng cách                                  │
│     - Tình trạng hoạt động                         │
│     - Số lượng cổng sạc trống                      │
│     - Thời gian chờ dự kiến                        │
│                                                    │
│     >>> BOTTLENECK                                 │
└────────────────────────────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────┐
│ [4] Di chuyển đến trạm và chờ sạc                  │
└────────────────────────────────────────────────────┘
```
Handoff: Người dùng tự tìm kiếm, tổng hợp thông tin
và quyết định lựa chọn trạm sạc.

Tổng thời gian: Chưa xác định (riêng bước 2–3
mất khoảng 5–30 phút/lượt).
* 🔴 **Bottleneck:** Thiếu thông tin tổng hợp về tình trạng trạm và khả năng phải chờ.
* 🔄 **Handoff:** Chưa đủ dữ liệu để xác định chính xác; riêng tìm kiếm và lựa chọn mất khoảng 15–30 phút/lượt.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Người sử dụng xe điện VinFast và tài xế Xanh SM. |
| **2. Current Workflow** | Kiểm tra SOC → tìm trạm sạc trên ứng dụng/bản đồ → tự đánh giá khoảng cách, tình trạng trạm và lựa chọn → di chuyển, chờ sạc. |
| **3. Bottleneck** | Tìm kiếm và so sánh các trạm sạc thủ công; thiếu thông tin tổng hợp về tình trạng hoạt động, mức độ đông và thời gian chờ dự kiến. |
| **4. Business Impact** | Mất 15–30 phút/lượt tìm kiếm và lựa chọn; tăng thời gian chờ, giảm hiệu suất sử dụng xe và trải nghiệm khách hàng. |
| **5. Success Metric** | Giảm thời gian tìm kiếm từ xuống ≤2 phút; giảm ít nhất 20% thời gian chờ sạc trung bình. |
| **6. Operational Boundary** | AI chỉ tìm kiếm, phân tích và đề xuất trạm phù hợp. Không tự ý đặt chỗ, điều hướng hoặc cam kết còn chỗ nếu chưa có dữ liệu xác thực. Người dùng quyết định trạm cuối cùng. |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [X] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.

```text
┌──────────────────────────────────────────────────────┐
│ [1] Người dùng nhập yêu cầu  (USER)                  │
│     - Vị trí hiện tại / Điểm đến                     │
│     - Mức pin (SOC)                                  │
└──────────────────────────────────────────────────────┘
                            │
                            ▼
┌──────────────────────────────────────────────────────┐
│ [2] AI thu thập dữ liệu  (AI)                        │
│     - Vị trí và khoảng cách                          │
│     - Trạng thái trạm sạc                            │
│     - Số cổng sạc đang trống                         │
│     - Lưu lượng và thời gian chờ                     │
└──────────────────────────────────────────────────────┘
                            │
                            ▼
┌──────────────────────────────────────────────────────┐
│ [3] AI đánh giá và xếp hạng trạm  (AI)               │
│     - Lọc trạm không phù hợp                         │
│     - Ước tính thời gian di chuyển                   │
│     - Dự đoán thời gian chờ                          │
│     - Đề xuất trạm tối ưu                            │
└──────────────────────────────────────────────────────┘
                            │
                            ▼
┌──────────────────────────────────────────────────────┐
│ [4] Người dùng xem và xác nhận  (USER)               │
│     - Xem danh sách đề xuất                          │
│     - So sánh các trạm                               │
│     - Chọn trạm phù hợp                              │
└──────────────────────────────────────────────────────┘
                            │
                            ▼
┌──────────────────────────────────────────────────────┐
│ [5] Điều hướng đến trạm sạc                          │
└──────────────────────────────────────────────────────┘
                            │
                            ▼
┌──────────────────────────────────────────────────────┐
│ [6] Sử dụng dịch vụ sạc                              │
└──────────────────────────────────────────────────────┘

╔══════════════════════════════════════════════════════╗
║ FALLBACK: nếu dữ liệu lỗi / thiếu / không cập nhật   ║
║   - Thông báo độ tin cậy của dữ liệu                 ║
║   - Hiển thị trạm gần nhất theo dữ liệu khả dụng     ║
║   - Cho phép người dùng tự tìm kiếm và lựa chọn      ║
╚══════════════════════════════════════════════════════╝
```
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 🏁 Phase 5 — EVALUATE 

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? Chưa xác minh dữ liệu thời gian thực về trạng thái trạm, số cổng sạc trống và thời gian chờ.
2. [X] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? Người dùng xác nhận trạm trước khi di chuyển, có fallback khi dữ liệu thiếu hoặc lỗi.
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? Chưa có bằng chứng xác nhận mức độ sẵn sàng.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[X] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> GO vì bài toán có quy trình rõ ràng, bottleneck cụ thể và
metric có thể đo lường (thời gian tìm kiếm, thời gian chờ).

Về kỹ thuật:
- Có thể sử dụng Rule Engine để lọc và xếp hạng trạm sạc.
- Có thể kết hợp dữ liệu thời gian thực để ước tính thời gian chờ.
- HITL và Fallback giúp kiểm soát rủi ro khi dữ liệu sai hoặc thiếu.
- Chưa cần triển khai Agentic AI hoặc LLM phức tạp.

Về chi phí:
- Prototype có thể giới hạn ở tìm kiếm và gợi ý Top 3 trạm.
- Tận dụng dữ liệu và API trạm sạc hiện có để giảm chi phí.
- Tránh chi phí LLM/Agent không cần thiết.

Điều kiện triển khai:
- Xác minh khả năng truy cập dữ liệu trạng thái trạm.
- Thu thập baseline thời gian tìm kiếm và chờ sạc.
- Thử nghiệm trên một khu vực trước khi mở rộng.
---