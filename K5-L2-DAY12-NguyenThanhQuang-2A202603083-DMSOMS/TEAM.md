# TEAM — Ngày 12

Mã bộ ảnh: **G06** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với | Số dòng disagreement |
|---|---|---|---|---:|
| Nguyễn Thanh Quang | 2A202603083 | Có | Trịnh Xuân Toàn · 2A202603121 (DMS/OMS) | 214 dòng gốc được giữ; 157 dòng đã được áp dụng/giữ trong v2, 57 dòng chờ Coach. |

## Trạng thái rework

`export_final_v2.zip` được dựng từ export đã commit và cập nhật các quyết định có căn cứ trong log. `check_final_v2.txt` ghi 22 ảnh, 0 lỗi và 1 cảnh báo D02 đã giải thích theo trục Y.

## Cần Coach xác nhận — chưa hỏi/chưa được xác nhận

- **DMS:** D02 `gaze_zone`/kính và trục landmark; D06 `eye_right` cùng cờ landmark; D01 các landmark mắt/miệng. V2 dùng giá trị thận trọng trong lúc chờ.
- **OMS:** S01, S03, S05, S06, S07 có occupant giống trẻ em; v2 không gán person/face cho occupant và dùng `occupied=unknown` khi cần.
- **E5:** slide 54 không có trong workspace hoặc repository. `class_list_v0.md` hiện theo GUIDE/schema và chờ Coach xác nhận cách đếm.
- **AI:** `prompts.md` khai rõ Codex đã hỗ trợ rà ảnh cục bộ. Bản ghi cũ nói có mentor cho phép; cần Coach xác nhận ngoại lệ này có phù hợp RULES §3 hay không. Không ghi nhận đã được Coach chấp thuận.

## Cá nhân

### NguyenThanhQuang-2A202603083

- Phần mình làm: gán nhãn bộ 22 ảnh G06; review chéo với Trịnh Xuân Toàn; rework export và lưu trạng thái các dòng E3.
- Điều mình học được: gọi ghế theo xe; phân biệt `infant_seat` với `child_seat`; không dùng màu IR-sim để suy nhãn; ảnh DMS xoay cần xét trái/phải theo người và trục Y.
