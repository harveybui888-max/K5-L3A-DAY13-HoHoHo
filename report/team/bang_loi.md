# Bảng lỗi và cách khắc phục · Nhiệm vụ C

> **Trạng thái hiện tại:** `PENDING – chờ nhãn độc lập và đối chiếu của hai thành viên`.
> Hai người gắn nhãn phải hoàn thành độc lập cả 20 ca trong ~8 phút, không trao đổi trước khi so sánh. File này chỉ chuẩn bị sẵn 20 mô tả gốc từ `docs/Ngay13_Lab13_De_bai_hoc_vien.docx` và cấu trúc bảng đối chiếu/khắc phục theo rubric; tuyệt đối không tự điền trước nhãn hoặc tỷ lệ đồng thuận.

## Định nghĩa 5 nhóm taxonomy chính thức (Google PAIR)

1. **Do người dùng:** Người dùng nhập sai dữ liệu, thao tác nhầm, chọn sai danh mục hoặc có kỳ vọng khác với thiết kế sản phẩm.
2. **Hệ thống:** Lỗi kỹ thuật/code/hạ tầng/tích hợp (API lỗi, cache cũ, thiếu khóa chống trùng, gọi sai tham số/tính sai quy tắc) đã hoặc có thể lộ ra trong vận hành.
3. **Ngữ cảnh:** Hệ thống hoạt động đúng kỹ thuật/chính sách nhưng thiếu hoặc lệch ngữ cảnh thực tế/giao tiếp/hiển thị (thời điểm gửi, thiếu giải thích cách tính, thông điệp ứng dụng mâu thuẫn).
4. **Giới hạn hệ thống:** Yêu cầu nằm ngoài phạm vi dữ liệu, kênh tiếp nhận hoặc nghiệp vụ mà trợ lý được thiết kế để xử lý (âm thanh, dữ liệu quá hạn, sản phẩm đối tác ngoài phạm vi).
5. **Ngầm:** Lỗi xảy ra âm thầm (sai tiền hoàn, tốn token bất thường, sai dữ liệu) nhưng hệ thống vẫn trả kết quả có vẻ bình thường, không kích hoạt cảnh báo và không ai nhận ra cho tới khi kiểm tra/audit.

## Hai bộ nhãn độc lập

Người gắn nhãn 1: Bùi Quang Huy (`2A202603469`) · Người gắn nhãn 2: Hoàng Minh Huy (`2A202603495`) (gắn trong 8 phút, không trao đổi)

| Ca | Mô tả tình huống (trích nguyên văn đề bài) | Nhãn người 1 | Nhãn người 2 | Lý do ngắn (Người 2) | Confidence | Trùng? | Nhãn thống nhất | Trạng thái |
| --: | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Khách nhập số tài khoản nhận hoàn tiền thiếu hai chữ số. Trợ lý tạo lệnh hoàn, ngân hàng trả về lỗi. | ... | ... | ... | ... | ... | ... | PENDING |
| 2 | Kiện nội địa 28 kg. Trợ lý gọi tool tra bảng giá với tham số hàng thường thay vì hàng nặng, hoàn thiếu 45.000 đ. Khách mở lại sau 2 ngày. | ... | ... | ... | ... | ... | ... | PENDING |
| 3 | Theo thiết kế, trợ lý hoàn tiền về ví LogiX trong 5 phút. Khách chờ tiền về tài khoản ngân hàng và báo “chưa được hoàn”. | ... | ... | ... | ... | ... | ... | PENDING |
| 4 | Khách yêu cầu hoàn phí cho chặng do hãng nước ngoài giao. LogiX không có dữ liệu chặng này. Trợ lý nói không xác định được trạng thái và chuyển cho nhân viên. | ... | ... | ... | ... | ... | ... | PENDING |
| 5 | Kiểm tra mẫu cuối tuần thấy 14 đơn có mã giảm giá bị hoàn theo giá trước giảm, thừa trung bình 12.000 đ mỗi đơn. Không khách nào báo, không cảnh báo nào kích. | ... | ... | ... | ... | ... | ... | PENDING |
| 6 | Khách chọn mục “Hoàn phí giao trễ” nhưng nội dung mô tả hàng bị vỡ. Trợ lý xử lý theo luồng giao trễ và từ chối vì đơn giao đúng hạn. | ... | ... | ... | ... | ... | ... | PENDING |
| 7 | API sổ cái trả lỗi 503 ở bước ghi hoàn tiền. Trợ lý thử lại 3 lần rồi vẫn báo khách “đã hoàn tiền thành công”. | ... | ... | ... | ... | ... | ... | PENDING |
| 8 | Trợ lý dẫn “Điều 7.2 chính sách hoàn phí” làm căn cứ. Bản chính sách hiện hành không có điều 7.2. Số tiền hoàn vẫn đúng. | ... | ... | ... | ... | ... | ... | PENDING |
| 9 | Khách nhập mã đơn của sàn thương mại điện tử thay vì mã vận đơn. Trợ lý báo “mã không hợp lệ” rồi dừng, không gợi ý gì. | ... | ... | ... | ... | ... | ... | PENDING |
| 10 | Đơn giao trễ do bão. Trợ lý từ chối hoàn theo điều khoản bất khả kháng, đúng chính sách. Khách thấy vô lý vì ứng dụng vẫn hiện “cam kết giao 24 giờ”. | ... | ... | ... | ... | ... | ... | PENDING |
| 11 | Khách gửi tin nhắn thoại 40 giây. Trợ lý không xử lý được âm thanh, trả lời “vui lòng nhập bằng chữ”. | ... | ... | ... | ... | ... | ... | PENDING |
| 12 | Tool tra đơn của depot D05 trả thiếu một trường. Trợ lý vẫn ra kết quả đúng sau nhiều lần gọi, nên tiền token của D05 gấp 3 lần depot khác suốt 3 tuần mà không ai thấy. | ... | ... | ... | ... | ... | ... | PENDING |
| 13 | Khách hỏi hoàn phí bảo hiểm hàng hoá, sản phẩm của công ty bảo hiểm đối tác, ngoài phạm vi trợ lý. Trợ lý trả lời chung chung về phí vận chuyển, không nói rõ là mình không xử lý được. | ... | ... | ... | ... | ... | ... | PENDING |
| 14 | Khách bấm nhầm “Xác nhận đã nhận tiền” khi chưa nhận. Yêu cầu bị đóng. | ... | ... | ... | ... | ... | ... | PENDING |
| 15 | Đơn trễ 26 giờ. Chính sách: trễ 24–48 giờ hoàn 50%. Trợ lý tính hoàn 100%. Nhân viên xem lại bắt được trước khi gửi. | ... | ... | ... | ... | ... | ... | PENDING |
| 16 | Theo thiết kế “gửi ngay khi xong”, trợ lý gửi thông báo hoàn tiền qua Zalo lúc 2:14 sáng. Khách phản ánh bị làm phiền. | ... | ... | ... | ... | ... | ... | PENDING |
| 17 | Bảng giá đổi từ ngày 01/11 nhưng trợ lý vẫn dùng bản cũ trong bộ nhớ đệm cho đơn dưới 2 kg. Lệch 1.000–2.000 đ mỗi đơn, 212 đơn trong 9 ngày, không ai mở lại. | ... | ... | ... | ... | ... | ... | PENDING |
| 18 | Trợ lý tính đúng: phí giao 30.000 đ, hoàn 50%. Tin nhắn chỉ ghi “Đã hoàn 15.000 đ”, không kèm cách tính. Khách cho là hoàn thiếu và mở lại yêu cầu. | ... | ... | ... | ... | ... | ... | PENDING |
| 19 | Khách yêu cầu hoàn phí cho đơn từ 14 tháng trước. Trợ lý chỉ truy cập được dữ liệu 12 tháng. Trợ lý nói rõ không tra được và chuyển cho nhân viên kèm tóm tắt. | ... | ... | ... | ... | ... | ... | PENDING |
| 20 | Khách gửi lại yêu cầu sau 10 phút vì chưa thấy phản hồi. Trợ lý hoàn hai lần cho cùng một đơn vì lệnh thứ hai không có khoá chống trùng. | ... | ... | ... | ... | ... | ... | PENDING |

**Công thức tỉ lệ đồng thuận:** `Số ca có Nhãn người 1 == Nhãn người 2 ÷ 20 × 100%` (yêu cầu đạt $\ge 16/20 = 80\%$).
**Tỉ lệ đồng thuận:** `PENDING` / 20 = `PENDING`%

## Quy tắc phân biệt cho các ca không trùng (Reconciliation)

Mỗi ca không trùng ghi một câu quy tắc phân biệt. Nếu đồng thuận dưới 80%, phải ghi định nghĩa đã viết lại trước khi gắn nhãn lại.

| Ca | Nhãn người 1 | Nhãn người 2 | Nhãn thống nhất | Quy tắc phân biệt (1 câu) |
| --: | --- | --- | --- | --- |
| `PENDING` | ... | ... | ... | `[CHỜ ĐỐI CHIẾU SAU KHI KHÓA 2 BỘ NHÃN]` |

## Bảng khắc phục cho 5 ca, mỗi loại một ca

> Yêu cầu rubric: chọn 5 ca đã thống nhất nhãn (mỗi nhóm taxonomy một ca); cách phát hiện phải đo được bằng event, ngưỡng và tần suất; người phụ trách là một vai trò cụ thể (không ghi "cả đội").

| Ca | Loại lỗi | Phát hiện bằng gì (event, ngưỡng, tần suất) | Chỉ số theo dõi | Khắc phục thế nào | Ai phụ trách |
| --: | --- | --- | --- | --- | --- |
| `PENDING` | Do người dùng | `[CHỜ chọn ca đại diện; xác định event + ngưỡng + tần suất]` | ... | ... | `[1 vai trò cụ thể, vd: Trưởng nhóm CSKH / Product Designer]` |
| `PENDING` | Hệ thống | `[CHỜ chọn ca đại diện; xác định event + ngưỡng + tần suất]` | ... | ... | `[1 vai trò cụ thể, vd: Kỹ sư Backend]` |
| `PENDING` | Ngữ cảnh | `[CHỜ chọn ca đại diện; xác định event + ngưỡng + tần suất]` | ... | ... | `[1 vai trò cụ thể, vd: PM trợ lý hoàn phí]` |
| `PENDING` | Giới hạn hệ thống | `[CHỜ chọn ca đại diện; xác định event + ngưỡng + tần suất]` | ... | ... | `[1 vai trò cụ thể, vd: Kỹ sư AI / PM trợ lý hoàn phí]` |
| `PENDING` | Ngầm | `[CHỜ chọn ca đại diện; xác định event + ngưỡng + tần suất]` | ... | ... | `[1 vai trò cụ thể, vd: Kế toán / Kiểm soát chất lượng]` |
