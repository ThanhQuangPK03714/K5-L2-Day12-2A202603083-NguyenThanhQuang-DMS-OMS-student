# Danh sách lớp v0 — Nguyễn Thanh Quang · G06

Bản nháp dựa trên GUIDE §4 và `labels_cabin_v1.json`; cần đối chiếu slide 54 trước khi nộp bản cuối.

## DMS

| STT | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---:|---|---|---|---|
| 1 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Gắn trạng thái dây an toàn với tài xế để cảnh báo bỏ quên/thắt sai; unknown tránh đoán khi không quan sát được. | Dây có thể chìm trong nền/tối; khi không thấy chọn unknown. |
| 2 | face.eye_left, face.eye_right | open / closed / unknown | Theo dõi trạng thái riêng từng mắt để phát hiện mắt nhắm; không suy ra buồn ngủ từ một khung. | Mắt có thể thấy, nhưng phản xạ NIR hoặc che khuất làm mất chi tiết. |
| 3 | face.glasses | none / clear / sun / unknown | Giúp diễn giải vùng mắt có kính và tránh nhầm kính với trạng thái mắt. | Khó phân biệt loại kính trên NIR; không rõ thì unknown. |
| 4 | face.gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Ước lượng vùng tài xế nhìn để nhận biết lúc nhìn lệch khỏi đường. | Hướng đầu có thể thấy; hướng mắt/đích nhìn có thể mơ hồ. |
| 5 | face13 | 13 điểm mặt; cờ occluded / outside | Định vị mắt, mũi, miệng để hỗ trợ theo dõi mặt; cờ biểu thị điểm không quan sát được. | Điểm có thể mất do phản xạ, tối hoặc vật che; không đặt điểm đoán. |
| 6 | hand.side, hand.on_wheel | left / right; yes / no / unknown | Theo dõi tay và việc tay chạm vô lăng để nhận biết thao tác của người lái. | Dạng/vị trí tay có thể thấy; tối hoặc che khuất làm không rõ. |
| 7 | phone.state | held / mounted / lap | Phát hiện điện thoại và trạng thái sử dụng để hỗ trợ nhận biết xao nhãng. | Có thể thấy hình dạng/vị trí; nếu vật không rõ thì không gán phone. |

## OMS

| STT | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---:|---|---|---|---|
| 1 | person.seat | driver / front_passenger / rear_left / rear_middle / rear_right | Xác định người ở ghế nào để gắn sự kiện với đúng vị trí trong xe. | Dáng người có thể thấy; ghế gọi theo xe, không theo trái/phải ảnh. |
| 2 | person.seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Theo dõi người ngồi xe có thắt dây phù hợp hay không. | Dây có thể chìm trong nền IR; không phân biệt được thì unknown. |
| 3 | child_seat.occupied | no / unknown | Phát hiện ghế trẻ em và trạng thái quan sát được để hỗ trợ nhắc kiểm tra ghế. | Hình ghế có thể thấy; nếu vùng ngồi bị che thì unknown. |
| 4 | infant_seat.facing | rear / front | Xác định hướng ghế em bé để hỗ trợ kiểm tra cách lắp ghế. | Hình dáng/hướng có thể thấy; trường hợp bị che cần xem xét. |
| 5 | object.type | bag / box / cup / other | Nhận dạng đồ vật để hỗ trợ phát hiện vật bị bỏ quên trong cabin. | Hình dạng/vị trí thường còn; không dựa vào màu trên IR. |
| 6 | frame_meta.modality, frame_meta.light | rgb / ir; day / night / unknown | Ghi bối cảnh cảm biến/ánh sáng để diễn giải dữ liệu và tránh nhầm khác biệt modality. | Đây là metadata khung hình; ảnh IR không giữ thông tin màu. |

## 2 câu hỏi leo thang

1. Câu hỏi: Với ảnh DMS xoay 90° và mắt bị che, khi nào nên đánh dấu điểm `occluded` và khi nào `outside` nếu không thể ước lượng vị trí?
   Khung ví dụ: D01.png.
   Tạm gán: mắt không phân biệt được thì `unknown`; cờ điểm theo khả năng quan sát thực tế; nếu không xác định được thì hỏi Coach trước khi sửa.
   Lý do: GUIDE §4.5–4.6 phân biệt trạng thái mắt với khả năng đặt từng điểm; trường hợp cụ thể cần xem ảnh.
2. Câu hỏi: Khi một vật nằm trong ghế trẻ em, có cần box `object` riêng cùng box ghế trong mọi trường hợp không?
   Khung ví dụ: S02_ir.png.
   Tạm gán: nếu Quang xác nhận có vật riêng biệt, dùng box riêng theo GUIDE §4.2; không kết luận vật có mặt chỉ từ tên khung.
   Lý do: guideline yêu cầu tách vật khỏi ghế; trường hợp khó nhận diện cần Coach xác nhận.

## 3. Xác nhận đối chiếu slide 54

- `frame_meta` không phải lớp đối tượng/box: đây là thẻ metadata của khung, gồm `modality`, `light`, `camera_blocked`.
- Không dùng `frame_meta` để cộng thêm lớp OMS đối tượng. Khi đối chiếu slide 54, số lớp đối tượng OMS thực tế trong danh sách này là `person`, `child_seat`, `infant_seat` và `object`; các thuộc tính `seatbelt`/`occupied`/`facing` là thuộc tính của lớp tương ứng.
- Nếu slide 54 quy định số mục OMS gồm metadata, đây là một mục bổ sung chứ không phải lớp đối tượng. Cần Coach xác nhận cách tính cuối trong buổi nộp; không tự đổi khái niệm.
