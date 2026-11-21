# Hồ sơ launch v0 · Trợ lý hoàn phí LogiX-VN · Gate 2a

> Tài liệu một trang phục vụ hội đồng Gate 2a duyệt kế hoạch **pilot** (không sử dụng cho triển khai chính thức). Cột trạng thái chỉ nhận: **Xong, có bằng chứng · Chưa · Giả lập**.

Nhóm: HoHoHo · Lớp: L3A (Thành viên: Bùi Quang Huy `2A202603469`, Hoàng Minh Huy `2A202603495`)

| Mục | Con số chính | Trạng thái | Người phụ trách |
| --- | --- | --- | --- |
| **1 · Chi phí mỗi việc thành công (A2, A3, A4)** | Toàn mẫu: **4.472 đ/việc thành công** (gấp `16,3x` hoá đơn token+tool `274,7 đ`). Theo loại: `noi_dia` **2.696 đ** (`0,22x`), `hang_nang` **8.221 đ** (`0,69x`), `doi_tac` **10.215 đ** (`0,85x`), `quoc_te` **22.515 đ** (`1,88x`, TC chỉ `27,3%`). Cộng cố định 40 triệu/tháng cho `noi_dia+hang_nang`: **4.599 đ** ở `45k yc/tháng` (`5.784 đ` ở nửa tải). | **Giả lập** *(tính từ `_simulated` trong CSV; số CP1 đã đối chiếu code & báo cáo)* | **Người kiểm số (CP1–CP2)** |
| **2 · Ba yếu tố nhạy nhất (B1, B2)** | (1) Số ca làm lại (`+51,8%` lên `6.787 đ` khi x2); (2) Tỉ lệ xem lại (`+40,7%` lên `6.292 đ` khi x2); (3) Lương nhân viên (`+23,1%` khi +25%). Chi phí thời gian nhân viên chiếm `92,5%` tổng chi phí. | **Giả lập** | **Người kiểm số (CP1–CP2)** |
| **3 · So với nhân viên tự làm `12.000 đ` (A3, B3, B4)** | Phạm vi `noi_dia+hang_nang` tiết kiệm rõ (`0,22x` và `0,69x`); giới hạn `k=2` lần chạy rẻ nhất toàn hệ thống (`6.901.220 đ`). **Điểm bất lợi:** nếu phải xem lại 100%, chi phí vọt lên **`11.743 đ` (`0,98x`)** hoặc **`12.415 đ` theo code / `12.414 đ` theo báo cáo (`1,03x`)** — mất lợi thế kinh tế. | **Giả lập** | **Người kiểm số (CP1–CP2)** |
| **4 · Chỉ số chính, chỉ số dùng, chỉ số an toàn (E1)** | Trên 1.200 yêu cầu mô phỏng: Chính (đóng 24h & không mở lại 7d) = **82,83%** (`994/1.200`); Dùng (gợi ý bị sửa/bỏ trên số xem lại) = **27,12%** (`48/177`); An toàn (mở lại 7d) = **4,25%** (`51/1.200`, trong phạm vi `noi_dia+hang_nang` là `3,97%`). Đã thiết kế 7 event có `trace_id`, `request_id`, `timestamp` *(chưa chạy tracking thực tế)*. | **Xong, có bằng chứng** *(số đo trên tập giả lập; schema event mới ở mức thiết kế)* | **PM trợ lý hoàn phí** |
| **5 · Bảng lỗi và cách khắc phục (CP3)** | **Đồng thuận 19/20 = 95%** (vượt ngưỡng $\ge 80\%$, chỉ bất đồng Ca 8: thống nhất xếp `Hệ thống` vì lỗi bịa điều khoản). Đã lập bảng khắc phục 5 ca đại diện 5 nhóm Google PAIR (Ca 1, 20, 18, 11, 5) với cách phát hiện đo được và người phụ trách cụ thể. | **Xong, có bằng chứng** | **Người gắn nhãn 2** |
| **6 · Pilot plan (CP4)** | Phạm vi thu hẹp `noi_dia + hang_nang`, `k=2`, chia theo `20 nhân viên can thiệp vs 20 nhân viên đối chứng` (phân tầng depot), rollout `4 -> 10 -> 20` nhân viên, chọn **MDE 6 điểm (`n_eff = 859/nhóm`, `m = 299 YC/NV`, `DEFF = 6,96`)** và 3 luật dừng định lượng. **Điểm bất lợi:** không đủ power ở MDE 5 điểm (trần `c/ICC = 1.000 < 1.251`; nếu hiệu ứng thật +5 điểm thì power chỉ còn `~0,64`). | **Xong, có bằng chứng** *(kế hoạch thiết kế, chờ xác nhận `decision_date`)* | **Giám đốc vận hành LogiX-VN** |
| **7 · Rủi ro kinh tế (E2)** | 3 rủi ro định lượng: làm lại x2 (`+51,8%` → `6.787 đ`), xem lại 100% kéo dài (`11.743–12.415 đ` ≥ mức `12.000 đ`), giảm tải còn một nửa (`+2.370 đ` chi phí cố định/việc; hòa vốn `4.659 việc/tháng`). | **Giả lập** | **PM trợ lý hoàn phí** |

---

**Đề xuất:** **Go có điều kiện** *(chỉ duyệt cho giai đoạn pilot phạm vi `noi_dia + hang_nang` với `k=2`; không duyệt cho `quoc_te` và không đánh giá cho chạy toàn bộ)*.

**Căn cứ (nêu cả số thuận lợi và bất lợi):**
- *Thuận lợi:* Phạm vi `noi_dia` (`2.696 đ = 0,22x`) và `hang_nang` (`8.221 đ = 0,69x`) cho chi phí mỗi việc thành công thấp hơn nhiều mức tự làm `12.000 đ`, kể cả khi cộng chi phí cố định `40 triệu/tháng` (`4.599 đ = 0,38x` ở `45k yc/tháng` [simulated]); đồng thuận phân loại lỗi đạt `95%` (`19/20`).
- *Bất lợi & Khoảng trống hiện tại:* (1) Còn các lỗi nghiêm trọng phát hiện ở CP3 chưa được vá trên hệ thống như hoàn tiền trùng lặp (Ca 20), lỗi API 503 vẫn báo thành công giả (Ca 7) và lỗi ngầm hoàn sai tiền mã giảm giá (Ca 5); (2) toàn bộ số chi phí hiện là **simulated**; (3) nếu phải xem lại 100%, CPS lên `11.743–12.415 đ` (`0,98x–1,03x`), không còn tiết kiệm; (4) thiết kế 20 nhân viên/nhóm phải đánh đổi MDE 6 điểm (`power ~0,64` nếu hiệu ứng thật là +5 điểm).

**Các điều kiện bắt buộc trước khi bấm nút chạy pilot:**
1. **Vá xong khóa chống trùng (`idempotency_key`, Ca 20), sửa xử lý lỗi API 503 (Ca 7) và thêm kiểm tra chặn hoàn vượt `paid_amount` (Ca 5)** — *Người phụ trách:* **Kỹ sư Backend** — *Ngày kiểm tra:* **Trước ngày khởi chạy pilot**.
2. **Ký xác nhận chấp nhận đánh đổi thống kê MDE 6 điểm** (`power = 0,64` tại mức chênh +5 điểm) và lịch chạy để đạt `m = 299` yêu cầu/nhân viên — *Người phụ trách:* **Giám đốc vận hành LogiX-VN** — *Ngày kiểm tra:* **Trước ngày khởi chạy pilot**.
3. **Triển khai đủ 7 event telemetry có `trace_id`, `request_id`, `timestamp`** (kèm event audit mẫu `audit_sample_checked`), thay số `_simulated` bằng thời gian đo thật sau tuần 1 và đảm bảo lộ trình giảm tỉ lệ xem lại `< 60%` (tránh kịch bản B4) — *Người phụ trách:* **PM trợ lý hoàn phí & Trưởng nhóm CSKH** — *Ngày kiểm tra:* **Cuối tuần 1 bước rollout 0.10**.
