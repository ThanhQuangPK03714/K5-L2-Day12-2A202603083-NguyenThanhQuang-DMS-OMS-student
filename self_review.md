# Tự rà soát — Nguyễn Thanh Quang · G06

## Nguồn và kiểm tra

Giữ `export_final.zip` làm bản ban đầu; tạo `export_final_v2.zip` từ bản rework được dựng lại trên cơ sở `HEAD:export_final.zip` và các quyết định trong log review. Checker hiện kiểm tra phạm vi nhãn theo GUIDE §4.1: face OMS chỉ là box; hand, phone và face13 không được xuất hiện trên ảnh SVIRO. Kết quả v2: 22 ảnh, 0 lỗi, 1 cảnh báo D02.

## OMS rework

- S01: infant seat `rear_right/facing=rear`; thêm object box ở `rear_middle`; bỏ nhãn DMS lọt vào SVIRO.
- S02: carrier `rear_right`; ghế trống `child_seat/rear_left`, `occupied=no`.
- S03: `child_seat/rear_middle`, `occupied=unknown`; thêm thùng `rear_right` và cốc `rear_left`; không gán occupant giống trẻ em thành person.
- S04: ghế trống `child_seat/rear_right`; cốc `rear_middle`; giữ người lớn `rear_left` và face box.
- S05: thêm cốc `rear_middle`; giữ người lớn `rear_left` và infant seat `rear_right`; không gán occupant trong carrier thành person.
- S06: giữ người lớn `rear_left` và `child_seat/rear_right`, `occupied=unknown`; bỏ nhãn DMS khỏi OMS.
- S07: hai box riêng — ghế trống `child_seat/rear_right`, `occupied=no`; ghế giữa `child_seat/rear_middle`, `occupied=unknown`; bỏ object box nhầm.
- S08: carrier trống `infant_seat/rear_right/facing=rear`; bỏ nhãn DMS khỏi OMS.

## DMS rework và cảnh báo

- D01: `eye_left=unknown`; landmark mắt không định vị chắc đánh `outside`; điểm miệng phía xa theo trạng thái ghi trong E3.
- D02: dùng `gaze_zone=other`; giữ mắt `unknown` và kính `unknown` trong lúc chờ Coach; tọa độ mắt giữ nguyên. Checker cảnh báo vị trí X, nhưng trên ảnh xoay 90° mắt trái có Y lớn hơn mắt phải theo GUIDE §3/CHECKPOINTS.
- D03: `gaze_zone=other`; giữ mắt/kính `unknown` do log ghi nhận phản xạ NIR làm mờ chi tiết.
- D05: `gaze_zone=other`; landmark vùng miệng bị chai che đánh `outside` theo review log.
- D06: `eye_right=unknown`, bốn landmark mắt phải `outside`; `gaze_zone=lap`; điểm miệng phía xa theo trạng thái E3.

## Việc cần Coach xác nhận

Chưa ghi là đã hỏi/đã được Coach xác nhận. Các ca cần xác nhận gồm D01 landmark; D02 gaze/kính và quy ước landmark; D06 mắt phải; occupant giống trẻ em ở S01/S03/S05/S06/S07; và việc dùng Codex rà ảnh cục bộ so với RULES §3. Các giá trị v2 là quyết định thận trọng tạm thời theo review log/GUIDE.

Slide 54 không có trong workspace/repository. `class_list_v0.md` đã tách `frame_meta` khỏi lớp đối tượng và theo GUIDE/schema; chưa thể ghi là đã đối chiếu slide 54.
