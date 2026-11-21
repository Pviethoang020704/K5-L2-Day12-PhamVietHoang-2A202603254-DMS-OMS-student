# Khai báo dùng AI — Phạm Việt Hoàng

Không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | ChatGPT | Giải thích yêu cầu bài; hướng dẫn CVAT; dịch nhãn/thuộc tính DMS/OMS; phân tích ERROR/WARN của `cabin_check.py`; giải thích review chéo; hướng dẫn cấu trúc báo cáo. | Dùng để hiểu quy trình và chuẩn bị nội dung biểu mẫu; không nhờ AI gán nhãn ảnh. | Có; đối chiếu README, GUIDE, RULES, CHECKPOINTS, schema và kết quả script. Không đưa ảnh cabin cho ChatGPT. |
| 2 | GitHub Copilot | Kiểm tra cấu trúc/dữ liệu export, đối chiếu diff, hoàn thiện biểu mẫu, kiểm tra tính nhất quán và chuẩn bị GitHub. | Chạy kiểm tra trên XML trong ZIP và log; soạn báo cáo dựa trên tài liệu/kết quả; không thay đổi annotation trong export hoặc script. | Có; chạy `cabin_check check`/`diff`, kiểm kê entry ZIP và đối chiếu tài liệu. Copilot không xem ảnh gốc, không trực tiếp quan sát hay gán nhãn ảnh. |
