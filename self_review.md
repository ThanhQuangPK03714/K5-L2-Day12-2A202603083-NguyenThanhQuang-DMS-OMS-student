# Tự đánh giá — Nguyễn Thanh Quang · G06

## 1. Tự rà soát 4 cảnh

Rà soát cấu trúc annotation trong `export_final.zip` và các báo cáo validator; đây chưa thay thế việc mở ảnh xem trực tiếp trong CVAT.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_ir.png | hand, face13 | extra | Export có nhãn DMS trên ảnh OMS; GUIDE §4.2 và §4.6 giới hạn hand/face13 cho DMS. Cần sửa trên CVAT sau khi xác nhận task. | Chưa |
| S01_rgb.png | face13 | extra | SVIRO chỉ dùng face box cho người lớn; không gán face13 trên S## (GUIDE §4.6). | Chưa |
| D01.png | mắt trái / face13 | flag | Validator báo eye_left=unknown nhưng chưa có cờ occluded/outside cho điểm mắt trái. Chưa xem ảnh để chọn cờ đúng. | Chưa |
| D06.png | mắt phải / face13 | flag | Validator báo eye_right=open trong khi cả bốn điểm phải đều bị đánh dấu che; cần kiểm tra trực tiếp và thống nhất trạng thái/cờ. | Chưa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Gán thành phần DMS (hand/face13) vào các khung OMS S## trong export hiện có.

Vì sao mình mắc: Có thể đã áp nhầm danh sách label DMS khi làm OMS; đây là giả thuyết từ cấu trúc export, cần tự xác nhận.

Lần sau tránh bằng cách: Trước mỗi khung kiểm tra loại task trong GUIDE §4.1–4.2; chỉ dùng face box trong OMS và không gán hand/face13 cho S##.

## 3. Ghi chú về disagreement_log

Bài học từ metadata modality: phải theo hậu tố `_rgb`/`_ir` và tạo frame_meta đầy đủ. Các kết luận về box, mắt và điểm mặt cần Quang xem trực tiếp trên CVAT trước khi chốt verdict.
