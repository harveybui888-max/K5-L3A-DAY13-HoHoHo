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

- **Công cụ sử dụng:** Trợ lý AI coding agent (Antigravity / Gemini 3.8 Flash).
- **Mục đích sử dụng:**
  - Hỗ trợ triển khai và tối ưu các hàm toán học xác suất chạy lại ở A1 (`so_lan_chay_ky_vong`, `ti_le_thanh_cong`, `he_so_chi_phi_moi_viec_thanh_cong`).
  - Hỗ trợ xây dựng hàm `mo_hinh()` linh hoạt với các tham số giá (`gia_vao`, `gia_ra`, `gia_tool`, `luong_phut`), hệ số xem lại/làm lại và giới hạn `max_lan_chay` để tự động hoá toàn bộ 9 kịch bản độ nhạy B1, kịch bản kép B2, đánh giá toàn hệ thống B3 và xem lại 100% B4.
  - Hỗ trợ viết script xử lý và kiểm tra dữ liệu bằng `pandas` (chú ý cờ `keep_default_na=False`, logic lọc attempt, gán chuyển nhân viên khi vượt giới hạn).
- **Cách tự kiểm tra và kiểm chứng kết quả:**
  - **Kiểm chứng tiên nghiệm (Unit tests A1):** Chạy hàm kiểm tra đáp án biết trước `kiem_tra_dap_an_biet_truoc()` với 3 phép thử ($1{,}20$ lần khi $k=2$; $1{,}25$ lần khi $k=\text{None}$; $1{,}25$ lần giá khi $k=3$ tại $p=0{,}8$), kết quả đạt $100\%$ (`assert` sai số $< 10^{-9}$).
  - **Tính toán đối chiếu bằng tay:** Tự tính tay công thức lý thuyết ($1/p = 1/0{,}8 = 1{,}25$), kiểm tra tính chất cộng tuyến tính ở kịch bản kép B2 ($+5{,}6\% + 40{,}7\% = +46{,}3\%$).
  - **Đối chiếu chéo với slide đáp án chuẩn:** Chạy `python src/lab13.py` và so sánh trực tiếp với tài liệu `docs/Lab13_Huong_dan_chi_tiet_buoi_chieu.md`: Mọi số liệu tại A2 (Token `245.585 đ`, Tool `84.000 đ`, Xem lại `1.780.000 đ`, Làm lại `2.264.000 đ`, Tổng `4.373.585 đ`, Thành công `978`, CPS `4.472 đ`), A3 (`noi_dia 2.696 đ`, `hang_nang 8.221 đ`, `quoc_te 22.515 đ`, `doi_tac 10.215 đ`), A4, B1 (9 kịch bản), B3 (k=2 rẻ nhất `6.901.220 đ`) đều khớp chính xác $100\%$ (độ lệch $0\% < 2\%$ cho phép).
  - **Kiểm tra kỷ luật báo cáo:** Rà soát thủ công để đảm bảo toàn bộ số liệu phát sinh từ cột giả lập đều có nhãn `simulated`, câu trả lời $\le 3$ dòng và chứa số liệu, tuân thủ nghiêm ngặt quy tắc 5 của lab (chỉ đánh giá pilot).

## 6. Tự đánh giá

- Hoàn thành gắn nhãn độc lập 20/20 ca lỗi CP3 (Người gắn nhãn 1) trong `report/team/bang_loi.md`, đạt đồng thuận **19/20 = 95%** với Người gắn nhãn 2.
