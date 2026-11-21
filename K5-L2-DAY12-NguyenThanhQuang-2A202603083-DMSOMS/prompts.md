# Khai báo dùng AI — Nguyễn Thanh Quang

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---:|---|---|---|---|
| 1 | ChatGPT / Codex | Theo yêu cầu của người học, hỗ trợ rà export G06, đối chiếu log/GUIDE, hoàn thiện rework v2 và hồ sơ E2–E5. | Đã hỗ trợ đọc ảnh G06 cục bộ trong lượt rà trước; dựng export v2 từ bản đã commit, cập nhật thuộc tính/box theo log và GUIDE, sửa checker để thực thi đúng phạm vi OMS/DMS §4.1, cập nhật hồ sơ và package. | Có: chạy `python -m scripts.cabin_check check .\export_final_v2.zip --expect 22 --manifest .\G06\oms\manifest.csv --out .\check_final_v2.txt`; 22 ảnh, 0 lỗi, 1 cảnh báo D02 được giải thích trong file. Đối chiếu với GUIDE và log review. |

## Xác nhận quy tắc sử dụng ảnh

Ảnh chỉ được xem cục bộ, không tải lên dịch vụ ngoài. Bản khai báo trước ghi rằng mentor đã cho phép lượt rà ảnh AI; tuy vậy RULES §3 cấm đưa ảnh cabin cho AI và chưa có xác nhận của Coach rằng trường hợp này được miễn. Để minh bạch, ghi nhận Coach confirmation đang chờ; không coi đây là đã được chấp thuận.
