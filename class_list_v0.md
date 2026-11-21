# Danh sách lớp v0 — Phạm Việt Hoàng · G01

Các giá trị và giới hạn quan sát dưới đây theo `labels_cabin_v1.json` và GUIDE.md. Khả năng nhìn thấy phụ thuộc từng ảnh; không phải kết luận đã quan sát các ảnh trong bộ.

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | `driver`, `front_passenger`, `rear_left`, `rear_middle`, `rear_right` | Xác định người thuộc vị trí nào để gắn thông tin DMS đúng người. | Có thể thấy người; vị trí ghế có thể khó khi ảnh tối hoặc bị che. |
| 2 | `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Theo dõi việc thắt dây an toàn của tài xế. | Dải dây có thể chìm vào nền/tối; không thấy rõ thì `unknown`. |
| 3 | `face.eye_left`, `face.eye_right` | `open`, `closed`, `unknown` | Theo dõi trạng thái mắt, hỗ trợ nhận biết dấu hiệu buồn ngủ. | Có thể thấy khe mắt; phản xạ/kính/che khuất làm khó phân biệt, khi đó `unknown`. |
| 4 | `face.gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Ước lượng vùng tài xế đang nhìn để nhận biết rời mắt khỏi đường. | Có thể hạn chế bởi bóng tối, phản xạ và hướng đầu; không chắc thì `other`. |
| 5 | `face.glasses` | `unknown`, `none`, `clear`, `sun` | Nhận biết kính đang đeo để diễn giải tín hiệu mắt phù hợp. | NIR có thể làm kính râm trông trong hơn; không rõ thì `unknown`. |
| 6 | `face13` | 13 điểm mặt; từng điểm có cờ `occluded`/`outside` | Định vị mắt, mũi, miệng phục vụ phân tích tư thế và trạng thái mặt. | Hình dạng có thể thấy nhưng landmark dễ bị che/phản xạ; mặt rộng dưới 60 px không gán `face13`. |
| 7 | `hand.on_wheel` | `yes`, `no`, `unknown` | Xác định tay tài xế có chạm vô lăng hay không. | Có thể nhận ra hình dáng tay; vùng tối/che khuất khiến kết luận tiếp xúc khó. |
| 8 | `phone.state` | `held`, `mounted`, `lap` | Phát hiện sử dụng điện thoại khi lái xe và vị trí sử dụng. | Chỉ gán khi thấy cạnh, góc hoặc màn hình; vật tối khó phân biệt thì không gán `phone`. |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | Các vị trí ghế trong schema | Đếm/ngữ cảnh người ngồi trong cabin và vị trí của họ. | Có thể nhận ra hình dáng người; ảnh IR tối có thể làm sót người hoặc khó gọi ghế. |
| 2 | `child_seat` | Có/không theo ghế; `occupied`: `no` hoặc `unknown` theo GUIDE | Nhận biết ghế trẻ em để quản lý bố trí/nhắc kiểm tra cabin. | Có thể thấy đường viền ghế; bên trong bị tối/che thì không kết luận trống. |
| 3 | `infant_seat` | `seat`; `facing`: `rear` hoặc `front` | Nhận biết nôi xách và hướng lắp để quản lý ghế an toàn. | Hình dạng có thể thấy nhưng hướng có thể mơ hồ; cần kiểm tra hình ảnh, không suy từ RGB/IR kia. |
| 4 | `object.type` | `bag`, `box`, `cup`, `other` | Nhận diện đồ vật để quản lý vật dụng trong cabin. | Có thể phân loại theo hình dạng/vị trí; không dùng màu trên IR, không chắc thì `other`. |
| 5 | `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Theo dõi dây an toàn của người ngồi trong cabin. | Dây có thể khó thấy trên ảnh IR; chỉ kết luận khi quan sát rõ. |
| 6 | `seat` (thuộc tính vị trí) | `driver`, `front_passenger`, `rear_left`, `rear_middle`, `rear_right` | Gắn người, ghế trẻ em, nôi và vật vào đúng vị trí trong xe. | Vị trí có thể thấy qua bố cục nhưng phải gọi theo xe; trái ảnh là phải xe khi camera nhìn về sau. |
| 7 | `frame_meta` | `modality`, `light`, `camera_blocked` | Ghi ngữ cảnh ảnh để diễn giải nhãn và kiểm soát dữ liệu đầu vào. | Loại ảnh lấy theo tên/nguồn; IR không cho suy màu hay thời điểm ngày đêm nếu không thấy bằng chứng. |

**Lưu ý về quy tắc:** JSON/schema hiện tại cho phép `child_seat.occupied=yes`, nhưng GUIDE §4.1 và §4.8 quy định chỉ dùng `no`/`unknown` và “không dùng `yes`”. Cần theo guideline lớp học và hỏi coach về sự không nhất quán; không sửa export bằng tay.

## 2 câu hỏi leo thang

1. Câu hỏi: GUIDE cho `infant_seat.facing` hai giá trị `front`/`rear` nhưng chưa nêu tiêu chí xử lý khi hướng ghế chỉ hiện một phần hoặc khó suy ra. Khi nào cần ghi nhận là ca mơ hồ và hỏi coach?  
   Khung ví dụ: `S07_ir.png` (diff ghi mine=`front`, peer=`rear`).  
   Bạn tạm gán thế nào và vì sao: Chưa chốt; mở ảnh trong CVAT để kiểm tra hướng lắp, không chọn theo peer hoặc IoU; hỏi coach nếu vẫn không rõ.
2. Câu hỏi: Với vật tối gần tay, cần thấy đặc điểm nào đủ để vẽ `phone` thay vì không gán điện thoại?  
   Khung ví dụ: `D05.png` (diff ghi hộp mine/peer lệch, IoU=0.23).  
   Bạn tạm gán thế nào và vì sao: Chỉ xác nhận `phone` nếu thấy cạnh, góc hoặc màn hình theo GUIDE §4.7; chưa xem ảnh nên trạng thái hiện là cần xác minh.
