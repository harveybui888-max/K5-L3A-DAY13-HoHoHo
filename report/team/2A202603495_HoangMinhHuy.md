# Báo cáo cá nhân — HoangMinhHuy-2A202603495

## 1. Thông tin thành viên

- Họ tên: Hoàng Minh Huy
- MSSV: 2A202603495
- Email: minhhuy108205@gmail.com
- GitHub: `hmhuyyy`
- Vai trong nhóm: **Người 2 — Risk, Pilot & Documentation Lead** (Người viết code tiếp quản CP4, Người gắn nhãn 2 kiêm giữ hồ sơ CP3–CP5)

## 2. Phần việc phụ trách

- Audit bàn giao CP1–CP2 của Người 1 (`e5353e2`) và kiểm thử tích hợp trong `src/.venv`.
- **CP3:** Chuẩn bị khung 20 ca lỗi, định nghĩa 5 nhóm Google PAIR, công thức đồng thuận và khung 5 biện pháp khắc phục trong `report/team/bang_loi.md` (giữ trạng thái `PENDING` chờ hai bộ nhãn độc lập).
- **CP4:** Tính cỡ mẫu cụm (D1), phân tích 7 khía cạnh identifiability (D2) và hoàn thiện `report/team/pilot_plan.yaml` (D3); bổ sung phần D1 vào `src/lab13.py`.
- **CP5:** Tính & chuẩn hóa 3 chỉ số E1 (xử lý right censoring 7 ngày), thiết kế 7 event có `trace_id`, hoàn thiện 3 rủi ro kinh tế E2 trong `report/team/chi_so.md`, tổng hợp `report/team/ho_so_launch_v0.md` (E3), `report/team/group_report.md` và `TEAM.md`.

## 3. Đóng góp cụ thể

- Dựng bản clone sạch từ fork, tạo nhánh `feature/person2-cp3-cp5` và môi trường ảo `src/.venv`.
- Triển khai D1 trong `src/lab13.py`: chứng minh MDE 5 điểm cần `1.251` mẫu hiệu dụng/nhóm (`3.103` thô / `42` NV/nhóm ở `m=75`), vượt quá 40 nhân viên và trần tiệm cận `20/0,02 = 1.000`; lựa chọn đánh đổi MDE 6 điểm (`859` mẫu hiệu dụng/nhóm, `m=299`, `DEFF=6,96`, `n_eff=859,20`) và ghi nhận minh bạch hạn chế `power = 0,64` nếu tác động thật là +5 điểm.
- Thiết kế 3 luật dừng 4 vế `NẾU – TRONG – THÌ – KHÔNG THÌ` dựa trên mức nền mô phỏng `mo_lai_trong_7_ngay` (`4,25%` toàn mẫu / `3,97%` trong phạm vi `noi_dia + hang_nang`) và chi phí CP1–CP2.
- Chuẩn hóa diễn giải chỉ số dùng `27,12%` (`48/177`) là tỉ lệ gợi ý bị sửa/bỏ trên số được xem lại, thiết kế 7 event có `trace_id`, `request_id`, `timestamp`, hoàn thiện 3 rủi ro E2 và đề xuất `Go có điều kiện` trong `ho_so_launch_v0.md`.

## 4. Bằng chứng

- Commit `d59a0be` (`feat: complete person 2 lab13 deliverables`) trên nhánh `feature/person2-cp3-cp5` và commit cập nhật hồ sơ thành viên.
- Các file đóng góp: `src/lab13.py` (phần D1 & D3/E1), `report/team/pilot_plan.yaml`, `report/team/chi_so.md`, `report/team/ho_so_launch_v0.md`, `report/team/bang_loi.md`, `report/team/group_report.md`, `TEAM.md`.
- Kiểm thử: `python lab13.py` chạy từ `src/` đạt exit code `0`; `yaml.safe_load` đọc `pilot_plan.yaml` hợp lệ, không còn `?` ngoài comment; kiểm tra từ cấm theo quy tắc 5 trong `report/team/` trả về `0` kết quả.

## 5. Công cụ AI đã dùng

- Sử dụng trợ lý AI coding agent (Antigravity / Gemini) để hỗ trợ audit bàn giao CP1–CP2, tính kiểm chứng công thức cỡ mẫu (`NormalDist` và `statsmodels.NormalIndPower`), kiểm tra CSV, rà soát YAML/rubric và soạn thảo cấu trúc tài liệu.
- **Cách tự kiểm tra:** Trực tiếp chạy lại `.\.venv\Scripts\python.exe lab13.py` trong `src/`, đối chiếu từng con số E1 từ `logix_requests.csv` (`994/1200 = 82,83%`, `48/177 = 27,12%`, `51/1200 = 4,25%`, `39/982 = 3,97%`), kiểm tra `yaml.safe_load`, kiểm tra `git diff --check` và xác minh không tự bịa nhãn CP3 hay kết quả duyệt chéo.

## 6. Tự đánh giá

- Hoàn thành đầy đủ và minh bạch phần CP4, CP5 và khung CP3 theo đúng rubric, bảo toàn thay đổi của Người 1 và không đưa số liệu giả vào các phần còn phụ thuộc con người (nhãn độc lập CP3 và duyệt chéo Gate 2a).
