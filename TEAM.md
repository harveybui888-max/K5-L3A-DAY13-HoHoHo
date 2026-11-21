# Team

## Thông tin nhóm

- Tên nhóm: HoHoHo
- Lớp: L3A
- Repo nhóm: `https://github.com/harveybui888-max/K5-L3A-DAY13-HoHoHo` *(lưu ý quy ước đặt tên theo `SUBMISSION.md`: `K5-L3A-DAY13-HoHoHo-LaunchEconomics`)*
- URL repo, nhánh nộp, commit chốt: `https://github.com/harveybui888-max/K5-L3A-DAY13-HoHoHo.git` · nhánh `feature/person2-cp3-cp5` (chờ merge vào `main` sau khi hoàn tất CP3 & duyệt chéo Gate 2a)

## Thành viên

> Nhóm gồm **2 thành viên** (đã phân công kiêm nhiệm 4 vai của lab; xác nhận với giảng viên/coach theo lưu ý `SUBMISSION.md`). Không khai báo thành viên ảo.

| STT | Họ tên | MSSV | Email | GitHub | Vai trò |
| --: | ------ | ---- | ----- | ------ | ------- |
|   1 | Bùi Quang Huy | 2A202603469 | harveybui888@gmail.com | harveybui888-max | Người 1 — Quantitative & Coding Lead (Người viết code CP1–CP2, Người kiểm số, Người gắn nhãn 1) |
|   2 | Hoàng Minh Huy | 2A202603495 | minhhuy108205@gmail.com | hmhuyyy | Người 2 — Risk, Pilot & Documentation Lead (Tiếp quản code CP4 D1, Người gắn nhãn 2 kiêm giữ hồ sơ CP3–CP5) |

Bốn vai của lab:

- **Người viết code:** Bùi Quang Huy viết và chạy phần CP1–CP2 trong `src/lab13.py`; Hoàng Minh Huy tiếp quản bổ sung phần CP4 (D1) và kiểm chứng D3/E1.
- **Người kiểm số:** Bùi Quang Huy đối chiếu bảng A1–A4, B1–B4 trong `report/team/bang_chi_phi.md`.
- **Người gắn nhãn 1:** Bùi Quang Huy (`CP3` — gắn nhãn độc lập 20 ca lỗi).
- **Người gắn nhãn 2, kiêm giữ hồ sơ:** Hoàng Minh Huy (`CP3` — gắn nhãn độc lập 20 ca lỗi; giữ và hoàn thiện `pilot_plan.yaml`, `chi_so.md`, `ho_so_launch_v0.md`, `group_report.md`).

## Cá nhân

Mỗi thành viên có báo cáo riêng trong `report/team/`:
- [report/team/2A202603469_BuiQuangHuy.md](report/team/2A202603469_BuiQuangHuy.md)
- [report/team/2A202603495_HoangMinhHuy.md](report/team/2A202603495_HoangMinhHuy.md)

## BuiQuangHuy-2A202603469

### Phần việc phụ trách

- CP1 (Nhiệm vụ A: A1, A2, A3, A4) — Mô hình chi phí mỗi việc thành công.
- CP2 (Nhiệm vụ B: B1, B2, B3, B4) — Phân tích độ nhạy 9 kịch bản, giới hạn chạy lại và xem lại 100%.
- Phối hợp gắn nhãn độc lập 20 ca lỗi CP3 (Người gắn nhãn 1) và kiểm tra chéo CP4–CP5.

### Đóng góp cụ thể

- Triển khai các hàm A1 (`so_lan_chay_ky_vong`, `ti_le_thanh_cong`, `he_so_chi_phi_moi_viec_thanh_cong`), hàm `mo_hinh` (A2), phân tách 4 loại yêu cầu (A3), chi phí cố định 40 triệu đ/tháng (A4) và toàn bộ phân tích độ nhạy B1–B4 trong `src/lab13.py`.
- Hoàn thiện bảng chi phí và độ nhạy trong `report/team/bang_chi_phi.md` với đầy đủ nhãn `simulated`.

### Bằng chứng

- Commit `e5353e2` (`feat: add lab13 implementation and team cost report(CP1,2)`) trên `main`.
- Chạy `python lab13.py`: `Ba phép thử đáp án biết trước: ĐẠT` (`1,20 · 1,25 · 1,25`); CPS toàn mẫu `4.472 đ` (`simulated`).

## HoangMinhHuy-2A202603495

### Phần việc phụ trách

- CP3 (Nhiệm vụ C) — Chuẩn bị biểu mẫu 20 ca lỗi, đối chiếu đồng thuận (sau khi khóa 2 bộ nhãn) và bảng khắc phục 5 nhóm.
- CP4 (Nhiệm vụ D: D1, D2, D3) — Tính cỡ mẫu cụm trong `src/lab13.py` và hoàn thiện `report/team/pilot_plan.yaml`.
- CP5 (Nhiệm vụ E: E1, E2, E3) — Đặc tả chỉ số, 7 event `trace_id`, 3 rủi ro kinh tế trong `report/team/chi_so.md`, hồ sơ `report/team/ho_so_launch_v0.md`, `report/team/group_report.md` và `TEAM.md`.

### Đóng góp cụ thể

- Audit bàn giao CP1–CP2 từ commit `e5353e2`, thiết lập branch `feature/person2-cp3-cp5` và môi trường `src/.venv`.
- Bổ sung code D1 (`co_mau`, DEFF, `n_eff`, giới hạn tiệm cận, power `0,64`) và thống kê D3/E1 vào `src/lab13.py`.
- Hoàn thiện `pilot_plan.yaml` (identifiability, rollout 4 → 10 → 20, 3 luật dừng 4 vế), `chi_so.md` (E1 có right censoring 7 ngày, 7 event có `trace_id`, E2 đủ 3 rủi ro), `ho_so_launch_v0.md` (đề xuất `Go có điều kiện`), `bang_loi.md` (khung `PENDING`) và `group_report.md`.

### Bằng chứng

- Commit `d59a0be` (`feat: complete person 2 lab13 deliverables`) trên nhánh `feature/person2-cp3-cp5` và commit cập nhật thông tin thành viên tiếp theo.
- `python lab13.py` chạy exit code `0`; `yaml.safe_load` hợp lệ, không còn `?` ngoài comment; 0 từ `production` trong `report/team/`.
