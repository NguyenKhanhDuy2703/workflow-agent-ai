# Khám phá dự án: mở rộng workflow BA → ticket

Status: draft. Date: 2026-11-06. Sources: [original input](requirements/system/discovery/input.md), [task request](requirements/task-ticketing/v1/request.md).

| Nội dung | Đã biết | Chưa biết / giới hạn |
| --- | --- | --- |
| Mục tiêu | Phân tích yêu cầu theo vai trò BA, đối chiếu design, đề xuất ticket vừa đủ nhỏ và có thể tạo trên nền tảng task | Chưa có bộ chỉ số đo hiệu quả; chất lượng đề xuất được đánh giá qua coverage, độ rõ AC và ranh giới ticket |
| Người dùng | Người giao việc/BA/PM và AI thực hiện workflow; người phát triển nhận ticket | Cơ cấu nhóm, người phụ trách, năng lực và lịch làm việc chưa cung cấp |
| MVP | Yêu cầu → ma trận đối chiếu → phân rã → kiểm tra chất lượng → preview; Trello là provider mặc định khi được yêu cầu publish | Lần này là phân tích thử; không tạo card thật |
| Ngoài MVP đề xuất | Đồng bộ hai chiều, dashboard mới, tự lập lịch sprint, tự chuyển Done, nhiều provider triển khai cùng lúc | Cần quyết định thêm nếu muốn mở rộng |
| Thời gian/chi phí | Không có giới hạn được cung cấp | Không tự suy ra deadline hoặc ngân sách từ ảnh |
| Dữ liệu | Requirements gốc, design version, source evidence, work item, cấu hình board/list, ticket draft và kết quả publish | Chưa có board/list hoặc tài liệu nghiệp vụ của tính năng thực tế để chạy BA |
| Môi trường | Hiện có các skill/command Markdown chạy qua AI; tài liệu NestJS là profile cho ứng dụng mục tiêu | Chưa có publisher thực thi. Đề xuất ưu tiên connector sẵn có, chỉ bổ sung helper khi năng lực connector không đủ |
| Tích hợp | Trello ban đầu chưa cài; lần kiểm tra cuối lượt xác nhận đã cài | Trạng thái xác thực, khả năng read/write thực tế và board access chưa được kiểm chứng; chưa có thao tác Trello live trong lượt này |

AI proposals: ưu tiên ticket có một kết quả kiểm chứng được; ước lượng mục tiêu khoảng 0,5–2 ngày công nếu đủ thông tin, không dùng như deadline hoặc luật cứng; provider độc lập với logic phân tích BA; mặc định preview trong tác vụ phân tích.

Unknowns không chặn bản phân tích: board/list, quy ước mã ticket, nhãn, người nhận việc, thời hạn và cách ước lượng của nhóm. Chúng chặn gán metadata/publish thật tương ứng. Không cần chọn frontend/backend/database mới để phân tích thủ tục.
