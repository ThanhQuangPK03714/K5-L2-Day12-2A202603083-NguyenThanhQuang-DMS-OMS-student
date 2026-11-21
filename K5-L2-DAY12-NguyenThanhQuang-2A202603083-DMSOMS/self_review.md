# Tự đánh giá — Nguyễn Thanh Quang · G06

## 1. Tự rà soát 4 cảnh

Đã rà soát cục bộ ảnh và annotation XML với Codex hỗ trợ sau khi mentor cho phép. Không sửa annotation trong CVAT/XML ở lượt review này.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | infant_seat / object | wrong_class / missing | Infant seat facing trong mine là front, hình carrier phù hợp rear; mine thiếu object box cho thùng ở ghế giữa. Peer phân loại object tốt hơn. | Chưa; cần sửa trên CVAT và export lại nếu Quang duyệt. |
| S03_rgb.png | infant_seat / child_seat | wrong_class | Mine gọi ghế là infant_seat; hình ghế có cánh đỡ là child_seat. Có occupant giống trẻ em; GUIDE yêu cầu báo Coach, không tự gán trẻ. Cả hai export dùng occupied=yes, ngoài schema. | Chưa. |
| D01.png | eye_left / face13 | flag | Mặt nghiêng và tối, mắt trái không thấy rõ nên unknown; các điểm trái thiếu cờ. Điểm không định vị được nên outside. | Chưa. |
| D06.png | eye_right / face13 | flag | Mắt phải phía xa không phân biệt; unknown an toàn hơn open. Điểm không định vị được nên outside. | Chưa. |

## 1A. Kết luận sau rà soát

Các thay đổi dưới đây đã được áp dụng vào `export_final.zip`:

| Trường hợp | Kết luận cuối | Cơ sở |
|---|---|---|
| S01_rgb.png | Infant seat giữ `rear`; không thêm `object` nếu vật không thể xác nhận riêng biệt. | Không có bằng chứng rõ ràng cho box vật riêng trong khung. |
| S03_rgb.png | Sửa ghế thành `child_seat`, `occupied=unknown`; dùng `unknown` thay vì giá trị `yes` không thuộc schema. | Hình ghế có cánh đỡ và vùng occupant không đủ rõ để khẳng định occupied. |
| D01.png | `eye_left=unknown`; bốn landmark mắt trái đặt `outside=1`. | Mặt nghiêng/tối, không thể xác nhận bốn điểm mắt trái. |
| D02.png | `gaze_zone=other` ở bản export tạm, thay cho center/road chưa phân biệt chắc. | Tư thế nghiêng và kính tối chưa đủ bằng chứng để chọn road hoặc center. |
| D06.png | `eye_right=unknown`; bốn landmark mắt phải đặt `outside=1`. Giữ `eye_left=open`. | Mắt trái phía gần quan sát được; mắt phải phía xa không phân biệt. |
| S02–S08_rgb.png | `frame_meta.light=unknown` cho ảnh RGB SVIRO dựng. | Quy tắc GUIDE về ảnh SVIRO, không có ánh sáng tự nhiên cần gán day/night. |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Gán nhầm lớp OMS và để nhãn DMS (hand/face13/thuộc tính face) xuất hiện trên S##; đồng thời thiếu một số object/person/face box và có box seat chưa đúng loại.

Vì sao mình mắc: Khả năng đã mang thói quen/lớp từ task DMS sang OMS và chưa rà từng ghế/vật theo xe trước khi export.

Lần sau tránh bằng cách: Trước mỗi ảnh xác nhận loại task, rà ba ghế sau theo xe, kiểm từng vật và chỉ dùng label theo GUIDE §4.1–4.3; chạy diff/check trước khi kết thúc.

## 3. Ghi chú về disagreement_log

Bài học: peer phân biệt infant_seat và child_seat đúng hơn ở S02/S04/S08, và tìm thấy các vật object bị mine bỏ sót. Diff chỉ chỉ ra nơi lệch; phải mở đúng ảnh, áp quy tắc lớp/ghế và không lấy đồng thuận làm chuẩn.
