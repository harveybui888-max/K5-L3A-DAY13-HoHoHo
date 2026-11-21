# Hồ sơ launch v0 · Trợ lý hoàn phí LogiX-VN · Gate 2a

> Tài liệu một trang phục vụ hội đồng Gate 2a duyệt kế hoạch **pilot** (không sử dụng cho triển khai chính thức). Cột trạng thái chỉ nhận: **Xong, có bằng chứng · Chưa · Giả lập** (các mục phụ thuộc nhãn độc lập CP3 ghi `PENDING` theo đúng hiện trạng).

Nhóm: HoHoHo · Lớp: L3A (Thành viên: Bùi Quang Huy `2A202603469`, Hoàng Minh Huy `2A202603495`)

| Mục | Con số chính | Trạng thái | Người phụ trách |
| --- | --- | --- | --- |
| **1 · Chi phí mỗi việc thành công (A2, A3, A4)** | Toàn mẫu: **4.472 đ/việc thành công** (gấp `16,3x` hoá đơn token+tool `274,7 đ`). Theo loại: `noi_dia` **2.696 đ** (`0,22x`), `hang_nang` **8.221 đ** (`0,69x`), `doi_tac` **10.215 đ** (`0,85x`), `quoc_te` **22.515 đ** (`1,88x`, TC chỉ `27,3%`). Cộng cố định 40 triệu/tháng cho `noi_dia+hang_nang`: **4.599 đ** ở `45k yc/tháng` (`5.784 đ` ở nửa tải). | **Giả lập** *(tính từ `_simulated` trong CSV; số CP1 đã đối chiếu code & báo cáo)* | **Người kiểm số (CP1–CP2)** |
| **2 · Ba yếu tố nhạy nhất (B1, B2)** | (1) Số ca làm lại (`+51,8%` lên `6.787 đ` khi x2); (2) Tỉ lệ xem lại (`+40,7%` lên `6.292 đ` khi x2); (3) Lương nhân viên (`+23,1%` khi +25%). Chi phí thời gian nhân viên chiếm `92,5%` tổng chi phí. | **Giả lập** | **Người kiểm số (CP1–CP2)** |
| **3 · So với nhân viên tự làm `12.000 đ` (A3, B3, B4)** | Phạm vi `noi_dia+hang_nang` tiết kiệm rõ (`0,22x` và `0,69x`); giới hạn `k=2` lần chạy rẻ nhất toàn hệ thống (`6.901.220 đ`). **Điểm bất lợi:** nếu phải xem lại 100%, chi phí vọt lên **`11.743 đ` (`0,98x`)** hoặc **`12.415 đ` theo code / `12.414 đ` theo báo cáo (`1,03x`)** — mất lợi thế kinh tế. | **Giả lập** | **Người kiểm số (CP1–CP2)** |
| **4 · Chỉ số chính, chỉ số dùng, chỉ số an toàn (E1)** | Trên 1.200 yêu cầu mô phỏng: Chính (đóng 24h & không mở lại 7d) = **82,83%** (`994/1.200`); Dùng (gợi ý bị sửa/bỏ trên số xem lại) = **27,12%** (`48/177`); An toàn (mở lại 7d) = **4,25%** (`51/1.200`, trong phạm vi `noi_dia+hang_nang` là `3,97%`). Đã thiết kế 7 event có `trace_id`, `request_id`, `timestamp` *(chưa chạy tracking thực tế)*. | **Xong, có bằng chứng** *(số đo trên tập giả lập; schema event mới ở mức thiết kế)* | **PM trợ lý hoàn phí** |
| **5 · Bảng lỗi và cách khắc phục (CP3)** | **PENDING – chờ nhãn độc lập và đối chiếu của hai thành viên** (đã chuẩn bị đủ 20 mô tả ca lỗi và khung 5 biện pháp theo taxonomy Google PAIR trong `bang_loi.md`, chưa có 2 bộ nhãn độc lập và tỉ lệ đồng thuận $\ge 80\%$). | **Chưa** *(PENDING)* | **Người gắn nhãn 2** |
| **6 · Pilot plan (CP4)** | Phạm vi thu hẹp `noi_dia + hang_nang`, `k=2`, chia theo `20 nhân viên can thiệp vs 20 nhân viên đối chứng` (phân tầng depot), rollout `4 -> 10 -> 20` nhân viên, chọn **MDE 6 điểm (`n_eff = 859/nhóm`, `m = 299 YC/NV`, `DEFF = 6,96`)** và 3 luật dừng định lượng. **Điểm bất lợi:** không đủ power ở MDE 5 điểm (trần `c/ICC = 1.000 < 1.251`; nếu hiệu ứng thật +5 điểm thì power chỉ còn `~0,64`). | **Xong, có bằng chứng** *(kế hoạch thiết kế, chờ xác nhận `decision_date`)* | **Giám đốc vận hành LogiX-VN** |
| **7 · Rủi ro kinh tế (E2)** | 3 rủi ro định lượng: làm lại x2 (`+51,8%` → `6.787 đ`), xem lại 100% kéo dài (`11.743–12.415 đ` ≥ mức `12.000 đ`), giảm tải còn một nửa (`+2.370 đ` chi phí cố định/việc; hòa vốn `4.659 việc/tháng`). | **Giả lập** | **PM trợ lý hoàn phí** |

---

**Đề xuất:** **Go có điều kiện** *(chỉ duyệt cho giai đoạn pilot phạm vi `noi_dia + hang_nang` với `k=2`; không duyệt cho `quoc_te` và không đánh giá cho chạy toàn bộ)*.

**Căn cứ (nêu cả số thuận lợi và bất lợi):**
- *Thuận lợi:* Phạm vi `noi_dia` (`2.696 đ = 0,22x`) và `hang_nang` (`8.221 đ = 0,69x`) cho chi phí mỗi việc thành công thấp hơn nhiều mức tự làm `12.000 đ`, kể cả khi cộng chi phí cố định `40 triệu/tháng` (`4.599 đ = 0,38x` ở `45k yc/tháng` [simulated]).
- *Bất lợi & Khoảng trống hiện tại:* (1) CP3 đang **PENDING** (chưa khóa 2 bộ nhãn độc lập và chưa có bảng khắc phục hoàn chỉnh cho các lỗi nghiêm trọng như hoàn trùng/lỗi 503 báo thành công giả); (2) toàn bộ số chi phí hiện là **simulated**; (3) nếu phải xem lại 100%, CPS lên `11.743–12.415 đ` (`0,98x–1,03x`), không còn tiết kiệm; (4) thiết kế 20 nhân viên/nhóm phải đánh đổi MDE 6 điểm (`power ~0,64` nếu hiệu ứng thật là +5 điểm).

**Các điều kiện bắt buộc trước khi bấm nút chạy pilot:**
1. **Hoàn tất CP3 (khóa 2 bộ nhãn độc lập $\ge 80\%$ đồng thuận & 5 biện pháp khắc phục),** đồng thời xử lý dứt điểm lỗi ghi nhận ở ca 7 (lỗi API 503 vẫn báo thành công) và ca 20 (thiếu khóa chống trùng) — *Người phụ trách:* **Kỹ sư Backend & Người gắn nhãn 2** — *Ngày kiểm tra:* **Trước ngày khởi chạy pilot (hạn khóa tại buổi bảo vệ Gate 2a / trước 2026-12-01)**.
2. **Ký xác nhận chấp nhận đánh đổi thống kê MDE 6 điểm** (`power = 0,64` tại mức chênh +5 điểm) và lịch chạy để đạt `m = 299` yêu cầu/nhân viên — *Người phụ trách:* **Giám đốc vận hành LogiX-VN** — *Ngày kiểm tra:* **Trước ngày khởi chạy pilot**.
3. **Triển khai đủ 7 event telemetry có `trace_id`, `request_id`, `timestamp`** trên hệ thống thử nghiệm và thay số `_simulated` bằng thời gian đo thật sau tuần 1; đảm bảo lộ trình giảm tỉ lệ xem lại `< 60%` (tránh kịch bản B4) — *Người phụ trách:* **PM trợ lý hoàn phí & Trưởng nhóm CSKH** — *Ngày kiểm tra:* **Cuối tuần 1 bước rollout 0.10**.
