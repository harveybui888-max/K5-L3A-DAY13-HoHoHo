# Phiếu chấm hội đồng Gate 2a

Nhóm số n chấm nhóm số n + 1; nhóm cuối chấm nhóm 1. Chấm theo bằng chứng trong hồ sơ, không theo cách trình bày: một đề xuất No-go có lý do bằng số được điểm cao hơn một đề xuất Go bỏ qua con số bất lợi.

- Nhóm chấm (hội đồng): HoHoHo (L3A — Bùi Quang Huy, Hoàng Minh Huy)
- Nhóm được chấm: Nhóm L3A-02 (theo phân công duyệt chéo $n \rightarrow n+1$)

| Tiêu chí | 0 điểm | 5 điểm | 10 điểm | Điểm | Lý do (có số) |
| --- | --- | --- | --- | ---: | --- |
| Đề xuất khớp bằng chứng | Mâu thuẫn với số của chính nhóm | Khớp nhưng bỏ qua một con số bất lợi | Khớp, nêu cả con số bất lợi và cách xử lý | **10** | Đề xuất "Go có điều kiện" hoàn toàn khớp với số liệu; không bỏ qua các con số bất lợi: chỉ ra CPS của đơn `quoc_te` lên tới 22.515 đ (1,88× so với mức tự làm 12.000 đ), tỉ lệ mở lại trong 7 ngày là 4,25% (3,97% trong phạm vi pilot), và rủi ro khi xem lại 100% đẩy chi phí lên 11.743–12.415 đ (0,98×–1,03×); đi kèm 4 điều kiện kỹ thuật cụ thể (vá khóa chống trùng, sửa lỗi sổ cái 503, chặn hoàn vượt tiền và telemetry) trước khi triển khai. |
| Số giả lập và phạm vi | Không nhãn; phạm vi "mọi yêu cầu" | Có nhãn hoặc có thu hẹp phạm vi | Nhãn ở mọi số giả lập; phạm vi thu hẹp có lý do bằng số | **10** | Đã gắn nhãn `[simulated]` tại 100% các ô số liệu có nguồn gốc từ cột `_simulated`; phạm vi thử nghiệm pilot được thu hẹp rõ ràng vào `noi_dia` (CPS 2.696 đ = 0,22×) và `hang_nang` (CPS 8.221 đ = 0,69×), loại bỏ dứt khoát `quoc_te` (tỉ lệ thành công chỉ 27,3%) và `doi_tac` (sát ngưỡng 0,85×) với đầy đủ cơ sở định lượng. |
| Pilot ra được quyết định | Không đối chứng hoặc thiếu cỡ mẫu | Đủ cỡ mẫu, luật dừng chung chung | Tách được tác động, đủ mẫu, luật dừng có ngưỡng, thời hạn, người có quyền dừng | **10** | Thiết kế pilot phân cụm ngẫu nhiên theo nhân viên (20 đối chứng vs 20 can thiệp, phân tầng theo 12 depot) giúp tách biệt tác động; tính đúng cỡ mẫu cụm với ICC = 0,02 (chỉ rõ MDE 5 điểm bị nghẽn trần tiệm cận 1.000 và chấp nhận đánh đổi sang MDE 6 điểm với $n_{\text{eff}} = 859$/nhóm); thiết lập đủ 3 luật dừng 4 vế NẾU – TRONG – THÌ – KHÔNG THÌ có ngưỡng định lượng (an toàn: mở lại > 6%, chi phí: CPS > 8.000 đ, sử dụng: tỉ lệ sửa/bỏ > 40%), thời hạn kiểm tra (tuần 1, tuần 2) và vai trò có thẩm quyền dừng (Trưởng ban Pilot / Giám đốc Vận hành). |
| **Tổng** | | | | **30 / 30** | |

**Quyết định của hội đồng:** **Go có điều kiện**

**Lý do:** Hồ sơ của nhóm được chấm đáp ứng xuất sắc các tiêu chí về phương pháp luận kinh tế lượng và kỹ thuật: số liệu trace minh bạch, gắn nhãn dữ liệu giả lập nghiêm ngặt, nhận diện trung thực các rủi ro kinh tế - vận hành và thiết kế kế hoạch thử nghiệm pilot có tính khả thi cao, bảo vệ an toàn cho doanh nghiệp.

**Một câu hỏi cho đội trình:** Với tỉ lệ mở lại đơn hiện tại là 4,25% trên toàn bộ mẫu (3,97% trong phạm vi nội địa + hàng nặng), nếu tuần đầu tiên nhóm chưa hoàn thiện hạ tầng telemetry để đo thời gian xem lại thực tế mà phải xem lại 100%, chi phí thực tế có vượt ngưỡng dừng an toàn 8.000 đ/yêu cầu không và nhóm xử lý phương án này thế nào?

**Câu trả lời của đội trình (ghi lại tại buổi):** Đội trình giải trình rằng trong tuần đầu tiên, nhóm không áp dụng xem lại 100% trên toàn bộ đơn mà triển khai chiến lược xem lại phân tầng dựa trên rủi ro (lấy mẫu ngẫu nhiên 30% kết hợp rà soát 100% đối với các đơn có số tiền hoàn lớn > 200.000 đ hoặc kiện hàng nặng), nhờ đó giữ chi phí biến đổi dưới 5.500 đ/việc thành công. Đồng thời, nhóm bố trí công cụ bấm giờ thủ công cho giám sát viên trong tuần 1 để ghi nhận số phút xem lại thực tế trước khi hệ thống telemetry tự động đi vào hoạt động ổn định.
