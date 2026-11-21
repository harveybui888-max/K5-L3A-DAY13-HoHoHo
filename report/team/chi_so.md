# Đặc tả chỉ số, event và rủi ro kinh tế · Nhiệm vụ E1, E2

## E1 · Đặc tả chỉ số

> **Lưu ý phương pháp:** Toàn bộ số liệu dưới đây được tính từ `src/logix_requests.csv` (1.200 yêu cầu **giả lập** trong bộ dữ liệu mô phỏng của lab, đọc bằng `keep_default_na=False`). Đây là kết quả quan sát trên bộ dữ liệu mô phỏng, **không phải** hiệu quả thực tế của một hệ thống đang vận hành, và **không** được kết luận trợ lý đã nâng chỉ số vì không có nhóm đối chứng.

| Loại | Chỉ số | Tử số & Mẫu số / Điều kiện hợp lệ (Right Censoring) | Tính thử trên 1.200 yêu cầu [simulated] | Nguồn, Tần suất & Owner |
| --- | --- | --- | --- | --- |
| Chính (kết quả) | % yêu cầu đóng trong 24 giờ và không mở lại trong 7 ngày | **Tử số:** `dong_trong_24h == 1` và `mo_lai_trong_7_ngay == 0`. **Mẫu số:** Tổng yêu cầu đã đóng đủ cửa sổ quan sát $\ge 7$ ngày (loại bỏ các yêu cầu mới chưa đủ 7 ngày để tránh right censoring). | **994 / 1.200 = 82,83%** | Event `request_closed` + `request_reopened`; Hằng tuần (chỉ tổng kết đủ 7 ngày); **PM trợ lý hoàn phí**; Mục tiêu pilot: `+6` điểm so với đối chứng |
| Dùng | Tỉ lệ gợi ý không được chấp nhận nguyên trạng (sửa hoặc bỏ) | **Tử số:** `quyet_dinh_xem_lai` là `sua` hoặc `bo`. **Mẫu số:** Số yêu cầu đã có quyết định xem lại (`duoc_xem_lai == 1`, có 177 ca). *Lưu ý: chỉ đo gợi ý bị sửa/loại bỏ sau khi xem, không đồng nghĩa tỉ lệ nhân viên phớt lờ không xem.* | **48 / 177 = 27,12%** | Event `staff_review_submitted`; Hằng ngày/tuần; **Trưởng nhóm CSKH**; Ngưỡng dừng cảnh báo: `> 40%` |
| An toàn | Tỉ lệ lỗi lọt đến khách (mở lại trong 7 ngày) | **Tử số:** `mo_lai_trong_7_ngay == 1`. **Mẫu số:** Tổng yêu cầu đã qua đủ $\ge 7$ ngày kể từ thời điểm đóng (loại ca chưa đủ 7 ngày do right censoring). | **51 / 1.200 = 4,25%** (trong phạm vi `noi_dia+hang_nang`: `39/982 = 3,97%`) | Event `request_reopened` + `request_closed`; Hằng ngày (cảnh báo 3 ngày liên tiếp); **Giám đốc vận hành LogiX-VN**; Ngưỡng dừng: cao hơn đối chứng $\ge 2$ điểm hoặc `> 6%` |
| Dùng (đề xuất) | Tỉ lệ gợi ý được nhân viên xem lại (Review Coverage) | **Tử số:** Số ca có `staff_review_submitted` (tương ứng `duoc_xem_lai == 1`). **Mẫu số:** Tổng số ca đã hiển thị gợi ý (`agent_suggestion_shown`) hoặc tổng yêu cầu nhóm can thiệp. | Tham khảo mẫu mô phỏng: 177 / 1.200 = 14,75% | Event `agent_suggestion_shown` + `staff_review_submitted`; Hằng tuần; **Trưởng nhóm CSKH** |
| An toàn (đề xuất) | Tỉ lệ chuyển nhân viên do hết lượt chạy (Escalation Rate) | **Tử số:** `ket_qua == 'chuyen_nhan_vien'`. **Mẫu số:** Tổng số yêu cầu gửi qua trợ lý trong ngày/tuần. | Tham khảo mẫu mô phỏng: không tính trong bảng chính | Event `agent_escalated_to_staff`; Hằng ngày; **Kỹ sư Backend** |

## Danh sách event (Schema đề xuất triển khai trong pilot)

> **Phân biệt hiện trạng:** Bộ dữ liệu CSV hiện tại (`logix_runs.csv`, `logix_requests.csv`) mới lưu trạng thái tổng hợp ở cấp bảng (`request_id`, `trace_id`, `attempt`, `status`, `dong_trong_24h`, `mo_lai_trong_7_ngay`, `quyet_dinh_xem_lai`). Các event dưới đây là **thiết kế schema telemetry đề xuất cần triển khai trong pilot**, **chưa** phải hệ thống đã ghi nhận thực tế. Mỗi event bắt buộc có `trace_id` và `request_id` (kèm `staff_id` khi có tương tác nhân viên) và `timestamp` để tính chính xác cửa sổ 24 giờ và 7 ngày.

| Event (đề xuất) | Ai tạo | Thuộc tính chính | Thời điểm phát sinh |
| --- | --- | --- | --- |
| `refund_request_received` | Hệ thống tiếp nhận (Gateway) | `request_id`, `depot`, `loai`, `so_tien_vnd`, `arm` (`treatment`/`control`), `timestamp`, `trace_id` | Ngay khi khách gửi yêu cầu hoàn phí |
| `agent_run_completed` | Dịch vụ Agent | `run_id`, `request_id`, `attempt`, `tokens_in`, `tokens_out`, `tool_calls`, `status` (`ok`/`loi`), `timestamp`, `trace_id` | Khi mỗi lần chạy của agent kết thúc |
| `agent_suggestion_shown` | Giao diện CSKH (Frontend) | `request_id`, `staff_id`, `suggestion_id`, `suggestion_amount`, `timestamp`, `trace_id` | Khi gợi ý của agent được hiển thị cho nhân viên |
| `agent_escalated_to_staff` | Dịch vụ Agent | `request_id`, `attempt_count`, `reason`, `timestamp`, `trace_id` | Khi agent chạy hết số lần tối đa (`k=2`) vẫn lỗi và chuyển cho nhân viên |
| `staff_review_submitted` | Giao diện CSKH (Nhân viên) | `request_id`, `staff_id`, `suggestion_id`, `quyet_dinh_xem_lai` (`giu`/`sua`/`bo`), `review_duration_sec`, `timestamp`, `trace_id` | Khi nhân viên hoàn tất xem lại và gửi/sửa/bỏ gợi ý |
| `request_closed` | Hệ thống quản lý đơn | `request_id`, `staff_id`, `resolution_channel`, `timestamp`, `trace_id` | Khi yêu cầu được đánh dấu đóng |
| `request_reopened` | Hệ thống quản lý đơn | `request_id`, `reopen_reason`, `timestamp`, `trace_id` | Khi khách hàng mở lại yêu cầu sau khi đóng |

**Kiểm tra chéo (Event ↔ Metric):**
- **Chỉ số chính (`% đóng 24h & không mở lại 7 ngày`):** Tính từ `request_closed.timestamp - refund_request_received.timestamp <= 24h` VÀ không phát sinh `request_reopened` có `request_reopened.timestamp - request_closed.timestamp <= 7 ngày` (nối theo `request_id` và `trace_id`; chỉ đưa vào mẫu số khi `now - request_closed.timestamp >= 7 ngày` để xử lý right censoring).
- **Chỉ số dùng (`Tỉ lệ gợi ý không được chấp nhận nguyên trạng`):** Đếm `staff_review_submitted` có `quyet_dinh_xem_lai in ['sua', 'bo']` chia tổng số `staff_review_submitted`.
- **Chỉ số an toàn (`Tỉ lệ mở lại trong 7 ngày`):** Đếm `request_reopened` thỏa mãn `<= 7 ngày` từ `request_closed.timestamp`, chia tổng số `request_closed` đã đủ cửa sổ 7 ngày.
- **Review Coverage (đề xuất):** Đếm `staff_review_submitted` chia tổng số `agent_suggestion_shown` (tỉ lệ xem lại trên số gợi ý hiển thị) hoặc tổng `refund_request_received` nhóm can thiệp.
- **Escalation Rate (đề xuất):** Đếm `agent_escalated_to_staff` chia tổng số `refund_request_received` nhóm can thiệp.

## E2 · Rủi ro kinh tế

> Toàn bộ số liệu định lượng dưới đây lấy trực tiếp từ kết quả CP1–CP2 (`src/lab13.py` và `report/team/bang_chi_phi.md`) trên dữ liệu giả lập (`simulated`). Không kết luận hiệu quả chỉ dựa vào CPS `< 12.000 đ` mà phải theo dõi đồng thời chi phí làm lại, xem lại, tỉ lệ thành công và an toàn.

| Rủi ro | Số liệu bằng chứng (`simulated`) | Nguyên nhân | Chỉ số theo dõi & Ngưỡng cảnh báo | Hành động ứng phó | Người phụ trách |
| --- | --- | --- | --- | --- | --- |
| **1. Số ca làm lại tăng gấp đôi** | CPS toàn mẫu tăng **+51,8%**, từ `4.472 đ` lên **`6.787 đ`** `[simulated]` (yếu tố nhạy thứ 1 ở B2; làm lại chiếm 51,8% tổng chi phí A2) | Trợ lý trả lời sai chính sách hoặc sai tham số khiến nhân viên phải xử lý lại từ đầu (`phut_lam_lai_simulated` cao) | **Chỉ số:** Tỉ lệ `lam_lai` theo tuần (mức mô phỏng trong phạm vi `noi_dia+hang_nang` là `4,89%` = 48/982). **Ngưỡng:** `> 7,0%` trong 1 tuần | Thu hẹp phạm vi về chỉ `noi_dia`, rà soát 20 trace `lam_lai` để sửa prompt/tool | **PM trợ lý hoàn phí** |
| **2. Tỉ lệ xem lại cao hoặc phải xem lại 100% kéo dài** | Xem lại x2 làm CPS tăng **+40,7%** lên **`6.292 đ`** `[simulated]` (B1/B2). Nếu phải xem lại 100% phạm vi `noi_dia+hang_nang`: CPS lên **`11.743 đ` (`0,98x`)** nếu làm lại 9p, hoặc **`12.415 đ` theo code / `12.414 đ` theo báo cáo (`1,03x`)** nếu làm lại 15,3p `[simulated]` (B4 — đắt hơn tự làm `12.000 đ`) | Nhân viên mất niềm tin hoặc quy trình bắt buộc duyệt tay 100% khiến chi phí nhân sự xem lại lấn át phần tiết kiệm | **Chỉ số:** Tỉ lệ xem lại (`Review Coverage`) và CPS thực tế tuần. **Ngưỡng:** Tỉ lệ xem lại `> 60%` hoặc CPS `> 8.000 đ` trong 7 ngày liên tiếp | Giảm tỉ lệ xem lại theo bậc với nhóm đơn an toàn khi `sua+bo < 15%`; kiểm soát thời gian xem lại `< 4,8 phút/ca`; kích hoạt luật dừng nếu vượt `8.000 đ` | **Trưởng nhóm CSKH** |
| **3. Khối lượng yêu cầu thấp hơn dự kiến làm chi phí cố định/việc tăng cao** | Chi phí cố định `40 triệu đ/tháng` cộng thêm **`1.185 đ/việc`** ở `45.000 yc/tháng` (tổng `4.599 đ` [simulated]), tăng lên **`2.370 đ/việc`** nếu giảm nửa còn `22.500 yc/tháng` (tổng `5.784 đ` [simulated]); mức hòa vốn là **`4.659 việc thành công/tháng`** (A4) | Lưu lượng thực tế hoặc mức độ sử dụng của nhân viên thấp không đủ gánh chi phí cố định vận hành trợ lý | **Chỉ số:** Số việc thành công/tuần và tỉ lệ sử dụng ở nhóm can thiệp. **Ngưỡng:** `< 50%` sản lượng dự kiến hoặc tỉ lệ dùng `< 50%` trong 7 ngày | Không mở rộng rollout, tìm nguyên nhân không dùng qua phỏng vấn nhân viên, rà lại cấu trúc chi phí cố định trước khi quyết định sau pilot | **Giám đốc vận hành LogiX-VN** |
