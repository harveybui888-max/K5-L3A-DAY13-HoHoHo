# Báo cáo nhóm

Báo cáo ngắn, tối đa 2 trang. Số liệu chi tiết nằm trong các file hồ sơ; ở đây chỉ dẫn lại con số chính.

## 1. Thông tin nhóm

- Tên nhóm: HoHoHo
- Lớp: L3A
- Thành viên: xem `TEAM.md` (1. Bùi Quang Huy — `2A202603469` · 2. Hoàng Minh Huy — `2A202603495`)

## 2. Mục tiêu và cách tiếp cận

Nhóm xây dựng hồ sơ đánh giá kinh tế và kế hoạch pilot (Gate 2a) cho trợ lý hoàn phí LogiX-VN trên tập dữ liệu mô phỏng (1.200 yêu cầu, 1.624 lần chạy). Công việc chia theo 2 đầu mối chính: Người 1 phụ trách mô hình chi phí và phân tích độ nhạy (`CP1–CP2`), Người 2 phụ trách phân loại lỗi, kế hoạch pilot, chỉ số vận hành và hồ sơ ra quyết định (`CP3–CP5`), cùng kiểm tra chéo trước khi tích hợp.

## 3. Giải pháp

- **Nhiệm vụ A & B (CP1–CP2):** Triển khai trong [src/lab13.py](../../src/lab13.py) và [bang_chi_phi.md](bang_chi_phi.md) (đạt 3 phép thử A1: `1,20 · 1,25 · 1,25`, mô hình chi phí theo trace, phân tách 4 loại yêu cầu, chi phí cố định 40 triệu đ/tháng, 9 kịch bản độ nhạy, giới hạn chạy lại `k=1,2,3` và kịch bản xem lại 100%).
- **Nhiệm vụ C (CP3):** Hai thành viên gắn nhãn độc lập 20 ca lỗi theo taxonomy 5 nhóm Google PAIR trong [bang_loi.md](bang_loi.md), đạt đồng thuận **19/20 = 95%**, thống nhất quy tắc phân biệt Ca 8 (`Hệ thống`) và lập bảng khắc phục 5 ca đại diện (Ca 1, 20, 18, 11, 5).
- **Nhiệm vụ D (CP4):** Bổ sung tính toán cỡ mẫu cụm (D1) vào `src/lab13.py`; thiết kế pilot theo nhân viên (`20` vs `20`, phân tầng theo depot), phân tích identifiability (D2) và 3 luật dừng định lượng trong [pilot_plan.yaml](pilot_plan.yaml).
- **Nhiệm vụ E (CP5):** Đặc tả chỉ số E1 (có xử lý right censoring 7 ngày), thiết kế 7 event có `trace_id`, phân tích 3 rủi ro kinh tế (E2) trong [chi_so.md](chi_so.md) và tổng hợp hồ sơ 7 mục trong [ho_so_launch_v0.md](ho_so_launch_v0.md).

## 4. Kết quả

- **Kinh tế (CP1–CP2):** Chi phí mỗi việc thành công toàn mẫu là `4.472 đ` (`simulated`), gấp `16,3x` hoá đơn token+tool (`274,7 đ`). Loại `noi_dia` (`2.696 đ = 0,22x`) và `hang_nang` (`8.221 đ = 0,69x`) tiết kiệm rõ rệt so với mức tự làm `12.000 đ`; loại `quoc_te` lỗ nặng (`22.515 đ = 1,88x`). Giới hạn chạy lại `k=2` cho chi phí toàn hệ thống thấp nhất (`6.901.220 đ` `[simulated]`). Xem lại 100% đẩy CPS lên `11.743–12.415 đ` (`0,98x–1,03x` `[simulated]`).
- **Chỉ số quan sát trên tập mô phỏng (E1):** Đóng trong 24h & không mở lại 7 ngày = `82,83%` (`994/1.200`); Gợi ý bị sửa/bỏ trên số được xem lại = `27,12%` (`48/177`); Mở lại trong 7 ngày = `4,25%` (`51/1.200`, phạm vi `noi_dia+hang_nang` là `3,97%`).
- **Phân loại lỗi (CP3):** Hai thành viên gắn nhãn độc lập đạt đồng thuận **19/20 = 95%** (chỉ khác Ca 8, thống nhất xếp `Hệ thống`).
- **Đề xuất Gate 2a:** **Go có điều kiện** cho pilot phạm vi `noi_dia + hang_nang` (`k=2`, MDE 6 điểm, `n_eff = 859/nhóm`), kèm điều kiện vá khóa chống trùng (Ca 20), sửa lỗi 503 báo thành công giả (Ca 7), kiểm tra chặn hoàn vượt `paid_amount` (Ca 5) và bật đủ 7 event telemetry.
- **Kết quả duyệt chéo hội đồng:** `PENDING` (chưa thực hiện phiên duyệt chéo với nhóm khác).

## 5. Khó khăn và cách xử lý

- Khởi đầu thư mục tải về ở dạng ZIP chưa có `.git` và chưa cài thư viện Python; nhóm đã clone lại từ repository fork, tạo branch `feature/person2-cp3-cp5` và thiết lập môi trường ảo `src/.venv` theo `src/requirements.txt`.
- Phát hiện sai số làm tròn nhỏ `1 đ` ở kịch bản B4 (`12.415 đ` trong `src/lab13.py` vs `12.414 đ` trong `bang_chi_phi.md`, lệch `0,008% < 2%`) và đã ghi nhận minh bạch trong hồ sơ.

## 6. Tổng hợp đóng góp

Chi tiết đóng góp của từng thành viên nằm trong [TEAM.md](../../TEAM.md) và hai báo cáo cá nhân: [2A202603469_BuiQuangHuy.md](2A202603469_BuiQuangHuy.md), [2A202603495_HoangMinhHuy.md](2A202603495_HoangMinhHuy.md).

## 7. Hạn chế và hướng cải thiện

- Dữ liệu hiện có là dữ liệu **giả lập** và không có nhóm đối chứng, nên chưa thể kết luận trợ lý cải thiện tỉ lệ đóng đơn thực tế.
- Với tối đa 40 nhân viên (20 cụm/nhóm) và `ICC = 0,02`, cỡ mẫu hiệu dụng bị chặn trên tại `1.000`, nên phải chấp nhận đánh đổi sang MDE 6 điểm (`power ~0,64` nếu tác động thật chỉ là +5 điểm).
- Cần hoàn tất triển khai 7 event telemetry thực tế và vá các lỗi nghiêm trọng phát hiện ở CP3 (Ca 5, Ca 7, Ca 20) trước khi chạy pilot.

## 8. Tài liệu tham khảo

- Tài liệu đề bài và hướng dẫn Lab 13 (`README.md`, `CHECKPOINTS.md`, `RUBRIC.md`, `docs/du_lieu_va_cong_thuc.md`, `docs/Lab13_Huong_dan_chi_tiet_buoi_chieu.md`).
- Erol et al., *Cost-of-Pass: An Economic Framework for Evaluating Language Models*, `arxiv.org/abs/2504.13359`.
- Google PAIR, *People + AI Guidebook*, chương "Errors + Graceful Failure".
