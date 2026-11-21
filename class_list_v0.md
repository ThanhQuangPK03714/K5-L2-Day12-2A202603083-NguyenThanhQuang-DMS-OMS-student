# Danh sách lớp v0 — Nguyễn Thanh Quang · G06

Bản này được rà theo `GUIDE.md` §4 và `labels_cabin_v1.json`. Slide 54 không có trong workspace/repository, nên chưa thể xác nhận đây là đối chiếu trực tiếp với slide; cần Coach kiểm tra phần E5 trước khi chốt.

## DMS

| STT | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---:|---|---|---|---|
| 1 | `person.seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Gắn trạng thái dây an toàn với tài xế để cảnh báo bỏ quên/thắt sai; `unknown` tránh đoán khi không quan sát được. | Dây có thể chìm trong nền/tối; khi không thấy chọn `unknown`. |
| 2 | `face.eye_left`, `face.eye_right` | open / closed / unknown | Theo dõi riêng từng mắt để phát hiện mắt nhắm; không suy ra buồn ngủ từ một khung. | Phản xạ NIR hoặc che khuất có thể làm mất chi tiết. |
| 3 | `face.glasses` | none / clear / sun / unknown | Diễn giải vùng mắt có kính và tránh nhầm kính với trạng thái mắt. | Khó phân biệt loại kính trên NIR; không rõ thì `unknown`. |
| 4 | `face.gaze_zone` | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Ước lượng vùng tài xế nhìn để nhận biết lúc nhìn lệch khỏi đường. | Hướng đầu có thể thấy; hướng mắt/đích nhìn có thể mơ hồ. |
| 5 | `face13` | 13 điểm mặt; cờ occluded / outside | Định vị mắt, mũi, miệng để hỗ trợ theo dõi mặt; cờ biểu thị điểm không quan sát được. | Điểm có thể mất do phản xạ, tối hoặc vật che; không đặt điểm đoán. |
| 6 | `hand.side`, `hand.on_wheel` | left / right; yes / no / unknown | Theo dõi tay và việc tay chạm vô lăng để nhận biết thao tác của người lái. | Dạng/vị trí tay có thể thấy; tối hoặc che khuất làm không rõ. |
| 7 | `phone.state` | held / mounted / lap | Phát hiện điện thoại và trạng thái sử dụng để hỗ trợ nhận biết xao nhãng. | Nếu hình dạng/vị trí không rõ thì không gán `phone`. |

## OMS

Các dòng dưới là sáu mục đầu ra lớp/thuộc tính dùng cho OMS; `frame_meta` được tách riêng và không tính là lớp đối tượng.

| STT | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---:|---|---|---|---|
| 1 | `person.seat` | driver / front_passenger / rear_left / rear_middle / rear_right | Xác định người ở ghế nào để gắn sự kiện với đúng vị trí trong xe. | Dáng người có thể thấy; ghế gọi theo xe, không theo trái/phải ảnh. |
| 2 | `person.seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Theo dõi người ngồi xe có thắt dây phù hợp hay không. | Dây có thể chìm trong nền IR; không phân biệt được thì `unknown`. |
| 3 | `face` (OMS box) | box-only; không có thuộc tính mắt/kính/gaze | Khoanh vùng mặt của người lớn được gán `person`, để dùng chung cấu trúc người/face giữa các khung. | Khuôn mặt có thể thấy; trong IR chi tiết mắt có thể kém rõ. |
| 4 | `child_seat.occupied` | no / unknown | Phát hiện ghế trẻ em và trạng thái quan sát được để hỗ trợ nhắc kiểm tra ghế. | Nếu vùng ngồi bị che hoặc không rõ thì `unknown`. |
| 5 | `infant_seat.facing` | rear / front | Xác định hướng ghế em bé để hỗ trợ kiểm tra cách lắp ghế. | Hình dáng/hướng có thể thấy; trường hợp bị che cần xem xét. |
| 6 | `object.type` | bag / box / cup / other | Nhận dạng đồ vật để hỗ trợ phát hiện vật bị bỏ quên trong cabin. | Hình dạng/vị trí thường còn; không dựa vào màu trên IR. |

## Metadata khung (không tính là lớp đối tượng)

`frame_meta` là tag của ảnh, gồm `modality` (rgb / ir), `light` (day / night / unknown) và `camera_blocked` (yes / no). Nó không phải box/lớp OMS.

## 2 câu hỏi leo thang

1. **D01/D02/D06:** Với ảnh DMS xoay 90° và điểm mặt khó định vị, khi nào đánh dấu `occluded`, khi nào `outside`? Mắt trái/phải của người lái được xét theo trục Y như thế nào trong ca mặt nghiêng?
   - Tạm áp dụng: chỉ gán `unknown` cho mắt không nhìn rõ; landmark không định vị chắc thì `outside`; ghi riêng trường hợp D02 trục Y. Cần Coach xác nhận các ca D01, D02 và D06.

2. **S01/S03/S05/S06/S07:** Khi SVIRO có occupant trông giống trẻ em, cần ghi nhận ghế và trạng thái occupied thế nào khi GUIDE nói không gán nhãn trẻ?
   - Tạm áp dụng: không tạo person/face cho occupant giống trẻ; giữ box ghế nếu nhìn thấy và `occupied=unknown` khi không thể xác nhận ghế trống. Cần Coach xác nhận các khung này.

## Đối chiếu slide 54

- `frame_meta` không được tính là lớp đối tượng; đây là tag metadata của khung.
- Các label OMS trong schema là `person`, `face`, `child_seat`, `infant_seat`, `object`. Bảng OMS có sáu dòng mục tiêu vì `person.seat` và `person.seatbelt` là hai thuộc tính/đầu ra riêng, không phải sáu label strings khác nhau.
- Chưa có slide 54 để xác minh cách giảng viên yêu cầu đếm các lớp/đầu ra E5. Chờ Coach xác nhận trước khi đổi tên hoặc gộp các mục.
