# TEAM — Ngày 12

Mã bộ ảnh: **G01** · Hình thức: **cá nhân**

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Phạm Việt Hoàng | 2A202603254 | có | Bùi Quốc Bình - 2A202603260 | 0/71 (71 phát hiện, 0 đã phân xử) |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Chưa có ca nào được xác nhận đã hỏi coach. 71 dòng diff còn cần đối chiếu trực quan trong CVAT.
- `S03_ir.png`, `S03_rgb.png`, `S05_ir.png`: mine ghi `child_seat.occupied=yes`; GUIDE §4.1 và §4.8 không cho phép `yes`, nhưng peer=`unknown` cũng chưa được xác nhận bằng ảnh. JSON/schema hiện tại lại cho phép giá trị `yes`.
- `S07_ir.png` và các ảnh liên quan: `infant_seat.facing` khác nhau (`front`/`rear`); cần xác minh hướng ghế trên ảnh và hỏi coach nếu vẫn không rõ.
- `D05.png`: vị trí/hộp `phone` khác nhau; cần kiểm tra vật thể có thấy cạnh, góc hoặc màn hình điện thoại không.

## Cá nhân

### PhamVietHoang-2A202603254
- Phần mình làm: đã gán đủ 22 ảnh và chạy self-check; đối chiếu lại export với peer bằng `cabin_check diff`.
- Điều mình học được hôm nay: PASS cấu trúc không đồng nghĩa mọi nhãn đã được phân xử; cần theo guideline và kiểm tra trực quan các ca mơ hồ.
