# Báo cáo cá nhân — BuiQuangHuy-2A202603469

## 1. Thông tin thành viên

- Họ tên: Bùi Quang Huy
- MSSV: 2A202603469
- Email: harveybui888@gmail.com
- GitHub: `harveybui888-max`
- Vai trong nhóm: **Người 1 — Quantitative & Coding Lead** (Người viết code phần CP1–CP2, Người kiểm số, Người gắn nhãn 1)

## 2. Phần việc phụ trách

- **CP1 (Nhiệm vụ A):** Xây dựng ba hàm A1 và mô hình chi phí từ trace (A2), phân tích theo 4 loại yêu cầu (A3) và chi phí cố định 40 triệu đ/tháng (A4).
- **CP2 (Nhiệm vụ B):** Phân tích độ nhạy 9 kịch bản (B1), đổi một cặp & xếp hạng 3 yếu tố ảnh hưởng mạnh nhất (B2), so sánh giới hạn chạy lại `k=1,2,3` (B3) và kịch bản xem lại 100% (B4).
- **CP3 & Kiểm tra chéo:** Tham gia gắn nhãn độc lập 20 ca lỗi (Người gắn nhãn 1) và đối chiếu số liệu tích hợp CP4–CP5.

## 3. Đóng góp cụ thể

- Hoàn thiện code CP1–CP2 trong `src/lab13.py` với đầy đủ tham số `gia_vao`, `gia_ra`, `gia_tool`, `luong_phut`, `he_so_xem_lai`, `he_so_lam_lai`, `max_lan_chay`.
- Hoàn thiện toàn bộ bảng A1–A4 và B1–B4 trong `report/team/bang_chi_phi.md`, gắn nhãn `simulated` cho các khoản tính từ `_simulated` và tính mức hoà vốn `4.659` việc thành công/tháng.
- Chỉ ra loại `quoc_te` không hiệu quả (`22.515 đ = 1,88×` [simulated], tỉ lệ thành công `27,3%`), giới hạn `k=2` rẻ nhất toàn hệ thống (`6.901.220 đ` [simulated]) và rủi ro khi xem lại 100% (`11.743–12.415 đ` [simulated]).

## 4. Bằng chứng

- Commit `e5353e2` (`feat: add lab13 implementation and team cost report(CP1,2)`) trên nhánh `main`.
- Kết quả chạy `src/lab13.py`:
  - `Ba phép thử đáp án biết trước: ĐẠT` (`1,20 · 1,25 · 1,25`).
  - A2: tổng chi phí `4.373.585 đ`, `978` việc thành công, CPS `4.472 đ` (`simulated`, gấp `16,3×` hoá đơn token+tool `274,7 đ`).
  - A3: `noi_dia 2.696 đ`, `hang_nang 8.221 đ`, `quoc_te 22.515 đ`, `doi_tac 10.215 đ` (`simulated`).
  - B1–B4: đủ 9 kịch bản, top 3 yếu tố nhạy nhất (số ca làm lại `+51,8%`, tỉ lệ xem lại `+40,7%`, lương nhân viên `+23,1%`), so sánh `k=1,2,3` và B4 xem lại 100%.

## 5. Công cụ AI đã dùng

- `[CHỜ Bùi Quang Huy điền công cụ AI đã sử dụng và cách tự kiểm tra kết quả CP1–CP2]`

## 6. Tự đánh giá

- `[CHỜ Bùi Quang Huy tự đánh giá và xác nhận sau khi hoàn tất gắn nhãn độc lập CP3]`
