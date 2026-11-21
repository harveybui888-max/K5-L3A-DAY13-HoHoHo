# Bảng lỗi và cách khắc phục · Nhiệm vụ C

> **Trạng thái hiện tại:** **Hoàn thành** — Đã khóa hai bộ nhãn độc lập 20/20 ca, tính tỉ lệ đồng thuận (**19/20 = 95%**), thống nhất quy tắc phân biệt ca bất đồng (Ca 8) và hoàn thiện bảng khắc phục 5 nhóm lỗi theo Google PAIR.

## Định nghĩa 5 nhóm taxonomy chính thức (Google PAIR)

1. **Do người dùng:** Người dùng nhập sai dữ liệu, thao tác nhầm, chọn sai danh mục hoặc có kỳ vọng khác với thiết kế sản phẩm.
2. **Hệ thống:** Lỗi kỹ thuật/code/hạ tầng/tích hợp (API lỗi, cache cũ, thiếu khóa chống trùng, gọi sai tham số/tính sai quy tắc, bịa điều khoản) đã hoặc có thể lộ ra trong vận hành.
3. **Ngữ cảnh:** Hệ thống hoạt động đúng kỹ thuật/chính sách nhưng thiếu hoặc lệch ngữ cảnh thực tế/giao tiếp/hiển thị (thời điểm gửi, thiếu giải thích cách tính, thông điệp ứng dụng mâu thuẫn).
4. **Giới hạn hệ thống:** Yêu cầu nằm ngoài phạm vi dữ liệu, kênh tiếp nhận hoặc nghiệp vụ mà trợ lý được thiết kế để xử lý (âm thanh, dữ liệu quá hạn, sản phẩm đối tác ngoài phạm vi).
5. **Ngầm:** Lỗi xảy ra âm thầm (sai tiền hoàn, tốn token bất thường, sai dữ liệu) nhưng hệ thống vẫn trả kết quả có vẻ bình thường, không kích hoạt cảnh báo và không ai nhận ra cho tới khi kiểm tra/audit.

## Hai bộ nhãn độc lập

Người gắn nhãn 1: Bùi Quang Huy (`2A202603469`) · Người gắn nhãn 2: Hoàng Minh Huy (`2A202603495`) (gắn độc lập trong 8 phút, không trao đổi trước khi so)

| Ca | Mô tả tình huống (trích nguyên văn đề bài) | Nhãn người 1 | Nhãn người 2 | Lý do ngắn (Người 2) | Confidence | Trùng? | Nhãn thống nhất |
| --: | --- | --- | --- | --- | --- | --- | --- |
| 1 | Khách nhập số tài khoản nhận hoàn tiền thiếu hai chữ số. Trợ lý tạo lệnh hoàn, ngân hàng trả về lỗi. | Do người dùng | Do người dùng | Khách nhập số tài khoản thiếu hai chữ số, dữ liệu đầu vào không chính xác. | Cao | Có | Do người dùng |
| 2 | Kiện nội địa 28 kg. Trợ lý gọi tool tra bảng giá với tham số hàng thường thay vì hàng nặng, hoàn thiếu 45.000 đ. Khách mở lại sau 2 ngày. | Hệ thống | Hệ thống | Trợ lý truyền sai tham số loại hàng khi gọi tool bảng giá, dẫn đến hoàn thiếu tiền. | Cao | Có | Hệ thống |
| 3 | Theo thiết kế, trợ lý hoàn tiền về ví LogiX trong 5 phút. Khách chờ tiền về tài khoản ngân hàng và báo “chưa được hoàn”. | Ngữ cảnh | Ngữ cảnh | Khách kỳ vọng nhận tiền vào tài khoản ngân hàng trong khi thiết kế hoàn về ví LogiX; thiếu thông tin làm rõ kênh nhận tiền. | Cao | Có | Ngữ cảnh |
| 4 | Khách yêu cầu hoàn phí cho chặng do hãng nước ngoài giao. LogiX không có dữ liệu chặng này. Trợ lý nói không xác định được trạng thái và chuyển cho nhân viên. | Giới hạn hệ thống | Giới hạn hệ thống | Chặng do hãng nước ngoài giao không có trong dữ liệu xử lý của LogiX. | Cao | Có | Giới hạn hệ thống |
| 5 | Kiểm tra mẫu cuối tuần thấy 14 đơn có mã giảm giá bị hoàn theo giá trước giảm, thừa trung bình 12.000 đ mỗi đơn. Không khách nào báo, không cảnh báo nào kích. | Ngầm | Ngầm | Hoàn tiền theo giá trước giảm gây sai số tiền nhưng không có cảnh báo, chỉ được phát hiện khi kiểm tra mẫu. | Cao | Có | Ngầm |
| 6 | Khách chọn mục “Hoàn phí giao trễ” nhưng nội dung mô tả hàng bị vỡ. Trợ lý xử lý theo luồng giao trễ và từ chối vì đơn giao đúng hạn. | Do người dùng | Do người dùng | Khách chọn nhầm danh mục giao trễ trong khi nội dung thực tế là hàng bị vỡ. | Trung bình | Có | Do người dùng |
| 7 | API sổ cái trả lỗi 503 ở bước ghi hoàn tiền. Trợ lý thử lại 3 lần rồi vẫn báo khách “đã hoàn tiền thành công”. | Hệ thống | Hệ thống | API sổ cái trả lỗi 503 nhưng trợ lý vẫn thông báo hoàn tiền thành công. | Cao | Có | Hệ thống |
| 8 | Trợ lý dẫn “Điều 7.2 chính sách hoàn phí” làm căn cứ. Bản chính sách hiện hành không có điều 7.2. Số tiền hoàn vẫn đúng. | Hệ thống | Ngữ cảnh | Số tiền đúng nhưng trợ lý viện dẫn điều khoản không tồn tại, khiến căn cứ giải thích không chính xác. | Trung bình | Không | Hệ thống |
| 9 | Khách nhập mã đơn của sàn thương mại điện tử thay vì mã vận đơn. Trợ lý báo “mã không hợp lệ” rồi dừng, không gợi ý gì. | Do người dùng | Do người dùng | Khách nhập mã đơn của sàn thương mại điện tử thay vì mã vận đơn. | Cao | Có | Do người dùng |
| 10 | Đơn giao trễ do bão. Trợ lý từ chối hoàn theo điều khoản bất khả kháng, đúng chính sách. Khách thấy vô lý vì ứng dụng vẫn hiện “cam kết giao 24 giờ”. | Ngữ cảnh | Ngữ cảnh | Quyết định từ chối đúng chính sách nhưng thông điệp cam kết giao 24 giờ trên ứng dụng tạo kỳ vọng trái chiều. | Cao | Có | Ngữ cảnh |
| 11 | Khách gửi tin nhắn thoại 40 giây. Trợ lý không xử lý được âm thanh, trả lời “vui lòng nhập bằng chữ”. | Giới hạn hệ thống | Giới hạn hệ thống | Trợ lý không hỗ trợ đầu vào âm thanh, yêu cầu nằm ngoài kênh xử lý được thiết kế. | Cao | Có | Giới hạn hệ thống |
| 12 | Tool tra đơn của depot D05 trả thiếu một trường. Trợ lý vẫn ra kết quả đúng sau nhiều lần gọi, nên tiền token của D05 gấp 3 lần depot khác suốt 3 tuần mà không ai thấy. | Ngầm | Ngầm | Tool thiếu trường khiến hệ thống gọi lại nhiều lần, làm chi phí token tăng bất thường nhưng không có cảnh báo. | Cao | Có | Ngầm |
| 13 | Khách hỏi hoàn phí bảo hiểm hàng hoá, sản phẩm của công ty bảo hiểm đối tác, ngoài phạm vi trợ lý. Trợ lý trả lời chung chung về phí vận chuyển, không nói rõ là mình không xử lý được. | Giới hạn hệ thống | Giới hạn hệ thống | Phí bảo hiểm của đối tác nằm ngoài phạm vi nghiệp vụ trợ lý được thiết kế để xử lý. | Cao | Có | Giới hạn hệ thống |
| 14 | Khách bấm nhầm “Xác nhận đã nhận tiền” khi chưa nhận. Yêu cầu bị đóng. | Do người dùng | Do người dùng | Khách bấm nhầm xác nhận đã nhận tiền, khiến yêu cầu bị đóng sai. | Cao | Có | Do người dùng |
| 15 | Đơn trễ 26 giờ. Chính sách: trễ 24–48 giờ hoàn 50%. Trợ lý tính hoàn 100%. Nhân viên xem lại bắt được trước khi gửi. | Hệ thống | Hệ thống | Trợ lý áp dụng mức hoàn 100% thay vì 50% theo chính sách trễ 24–48 giờ. | Cao | Có | Hệ thống |
| 16 | Theo thiết kế “gửi ngay khi xong”, trợ lý gửi thông báo hoàn tiền qua Zalo lúc 2:14 sáng. Khách phản ánh bị làm phiền. | Ngữ cảnh | Ngữ cảnh | Thông báo được gửi lúc 2:14 sáng theo logic gửi ngay nhưng không xét đến thời điểm phù hợp với khách hàng. | Cao | Có | Ngữ cảnh |
| 17 | Bảng giá đổi từ ngày 01/11 nhưng trợ lý vẫn dùng bản cũ trong bộ nhớ đệm cho đơn dưới 2 kg. Lệch 1.000–2.000 đ mỗi đơn, 212 đơn trong 9 ngày, không ai mở lại. | Ngầm | Ngầm | Cache sử dụng bảng giá cũ gây sai lệch trên nhiều đơn nhưng không kích hoạt cảnh báo. | Cao | Có | Ngầm |
| 18 | Trợ lý tính đúng: phí giao 30.000 đ, hoàn 50%. Tin nhắn chỉ ghi “Đã hoàn 15.000 đ”, không kèm cách tính. Khách cho là hoàn thiếu và mở lại yêu cầu. | Ngữ cảnh | Ngữ cảnh | Số tiền hoàn đúng nhưng thiếu giải thích cách tính khiến khách hiểu nhầm là hoàn thiếu. | Cao | Có | Ngữ cảnh |
| 19 | Khách yêu cầu hoàn phí cho đơn từ 14 tháng trước. Trợ lý chỉ truy cập được dữ liệu 12 tháng. Trợ lý nói rõ không tra được và chuyển cho nhân viên kèm tóm tắt. | Giới hạn hệ thống | Giới hạn hệ thống | Yêu cầu vượt quá cửa sổ dữ liệu 12 tháng mà trợ lý có thể truy cập. | Cao | Có | Giới hạn hệ thống |
| 20 | Khách gửi lại yêu cầu sau 10 phút vì chưa thấy phản hồi. Trợ lý hoàn hai lần cho cùng một đơn vì lệnh thứ hai không có khoá chống trùng. | Hệ thống | Hệ thống | Thiếu khóa chống trùng khiến cùng một yêu cầu tạo hai lệnh hoàn tiền. | Cao | Có | Hệ thống |

**Công thức tỉ lệ đồng thuận:** `Số ca có Nhãn người 1 == Nhãn người 2 ÷ 20 × 100%` (yêu cầu đạt $\ge 16/20 = 80\%$).
**Tỉ lệ đồng thuận:** **19 / 20 = 95%** (Đạt chuẩn $\ge 80\%$).

## Quy tắc phân biệt cho các ca không trùng (Reconciliation)

| Ca | Nhãn người 1 | Nhãn người 2 | Nhãn thống nhất | Quy tắc phân biệt (1 câu) |
| --: | --- | --- | --- | --- |
| 8 | Hệ thống | Ngữ cảnh | **Hệ thống** | Khi trợ lý tự bịa hoặc trích dẫn sai điều khoản không tồn tại trong văn bản chính sách hiện hành (dù số tiền đúng), gắn nhãn **Hệ thống** vì nguyên nhân gốc là lỗi sinh nội dung/truy xuất tri thức của mô hình chứ không phải thiếu ngữ cảnh giao tiếp. |

## Bảng khắc phục cho 5 ca, mỗi loại một ca

> Mỗi loại chọn 1 ca đã thống nhất nhãn; cách phát hiện đo được bằng event, ngưỡng và tần suất; mỗi dòng có đúng 1 vai trò phụ trách.

| Ca | Loại lỗi | Phát hiện bằng gì (event, ngưỡng, tần suất) | Chỉ số theo dõi | Khắc phục thế nào | Ai phụ trách |
| --: | --- | --- | --- | --- | --- |
| 1 | Do người dùng | Event `agent_run_completed` (`error_type == 'invalid_bank_account'`) vượt ngưỡng `> 3%` tổng yêu cầu trong ngày (kiểm tra hằng ngày) | Tỉ lệ yêu cầu lỗi định dạng tài khoản ngân hàng / ngày | Kiểm tra độ dài và định dạng số tài khoản ngay trên giao diện nhập trước khi tạo lệnh hoàn; hiển thị gợi ý số chữ số chuẩn theo ngân hàng | **Product Designer** |
| 20 | Hệ thống | Event `refund_ledger_write` / `agent_run_completed` phát hiện `>= 1` đơn có `>= 2` lệnh hoàn tiền thành công cho cùng `request_id`/`order_id` trong 24h (cảnh báo tức thời & tổng kết hằng ngày) | Số ca hoàn tiền trùng lặp (ngưỡng dừng pilot: `>= 1 ca`) | Bắt buộc gắn khóa chống trùng (`idempotency_key` theo `order_id` + `refund_type`) ở dịch vụ sổ cái và chặn gửi yêu cầu mới khi lệnh cũ đang xử lý | **Kỹ sư Backend** |
| 18 | Ngữ cảnh | Event `request_reopened` với `reopen_reason == 'disputed_amount'` trên các đơn tính đúng, vượt ngưỡng `> 2%` số đơn đã đóng trong tuần (kiểm tra hằng tuần) | Tỉ lệ mở lại do khiếu nại số tiền dù tính đúng | Cập nhật mẫu tin nhắn phản hồi bắt buộc ghi rõ công thức (`Phí giao × tỉ lệ hoàn = số tiền`) và dẫn chiếu điều khoản chính sách áp dụng | **PM trợ lý hoàn phí** |
| 11 | Giới hạn hệ thống | Event `agent_escalated_to_staff` có `reason == 'unsupported_audio_input'` vượt ngưỡng `> 5%` tổng yêu cầu trong tuần (kiểm tra hằng tuần) | Tỉ lệ yêu cầu âm thanh bị từ chối hoặc chuyển nhân viên | Tự động nhận diện tệp âm thanh ở cổng tiếp nhận và định tuyến thẳng tới hàng đợi CSKH kèm hướng dẫn gửi chữ nếu khách muốn xử lý nhanh | **Kỹ sư AI** |
| 5 | Ngầm | Event `audit_sample_checked` đối soát ngẫu nhiên tối thiểu 50 đơn/tuần; kích hoạt cảnh báo khi phát hiện `>= 1` đơn có `|so_tien_da_hoan - so_tien_dung| > 1.000 đ` (kiểm tra hằng tuần) | Tỉ lệ đơn sai số tiền qua mẫu audit tuần & tổng tiền chênh lệch (đ) | Sửa công thức tính hoàn phí theo giá thực trả sau mã giảm giá; thêm bước kiểm tra tự động chặn mọi lệnh hoàn vượt quá số tiền khách đã thanh toán | **Kế toán kiểm soát chất lượng** |
