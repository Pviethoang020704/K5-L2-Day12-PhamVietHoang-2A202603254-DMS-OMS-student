# Tự đánh giá — Phạm Việt Hoàng · G01

## 1. Tự rà soát 4 cảnh

Các ghi chú dưới đây dựa trên `disagreement_log.csv`, không phải kết quả xem lại ảnh. Tôi chưa mở ảnh cabin bằng AI và chưa xác nhận trực quan trong CVAT.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| D02.png | `face.eye_left`, `face.eye_right`, `face13` | `guess`, `flag` | Diff ghi mắt `open`/`unknown` và khác cờ `occluded`; cần kiểm xem khe mắt có thấy rõ và từng điểm có bị che không. | Chưa xác minh; chưa sửa |
| D05.png | `phone`, `face`, `face13` | `box`, `guess`, `missing` | Diff ghi hai bất đồng về hộp `phone` (mine IoU=0.23 và một hộp chỉ có ở peer), cùng khác biệt mắt/vùng nhìn và số skeleton. Cần kiểm cạnh/góc/màn hình điện thoại và từng đối tượng trên ảnh. | Chưa xác minh; chưa sửa |
| S03_ir.png | `child_seat.occupied`, `object.type` | `wrong_class`, `guess` | Diff ghi mine=`yes`, peer=`unknown` và `other`/`bag`. Theo GUIDE §4.8 không dùng `occupied=yes`; cần xem ghế có nhìn rõ bên trong không và hình dạng đồ vật trước khi chọn `no`/`unknown` hoặc `bag`/`other`. | Chưa xác minh; chưa sửa |
| S07_ir.png | `infant_seat.facing` | `wrong_class` | Diff ghi mine=`front`, peer=`rear`; log không cho biết hướng nào đúng và guideline chưa nêu tiêu chí phân xử hình ảnh cụ thể. | Chưa xác minh; chưa sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Chưa đủ bằng chứng để kết luận có lỗi cá nhân lặp lại. Diff cho thấy nhiều bất đồng về mức độ nhìn rõ mắt và các điểm `face13`.

Vì sao mình mắc: Chưa kiểm tra lại các khung này trực quan trong CVAT; không thể xác định nguyên nhân từ CSV diff hoặc IoU.

Lần sau tránh bằng cách: Mở ảnh gốc trong CVAT local, kiểm từng mắt/điểm theo GUIDE §4.5–§4.6, dùng `unknown` khi không phân biệt được và chỉ đánh dấu đã sửa sau khi export/check lại.

## 3. Ghi chú về disagreement_log

Chưa thể xác nhận dòng nào peer đúng và mình sai khi chưa xem ảnh. Đặc biệt, giá trị mine=`child_seat.occupied=yes` vi phạm GUIDE §4.1/§4.8, nhưng cần xem ảnh để quyết định giá trị thay thế; không xem `peer=unknown` là đã được phân xử.
