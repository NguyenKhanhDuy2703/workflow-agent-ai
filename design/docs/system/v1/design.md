# System v1: workflow và phần mở rộng tạo ticket

Status: draft. Approved by/date: unset. Date: 2026-11-06.

Sources: [system input v1](../../../requirements/system/v1/input.md), [discovery](../../../discovery.md), current [rules](../../../../RULES.md) and [guide](../../../../AGENTS.md).

## Phạm vi và hiện trạng

Hệ thống đang có là tập thủ tục cho AI: skill điều phối stage, command mô tả bước, tài liệu profile NestJS. Chưa có application source, executable helper, task-provider adapter, nguồn dữ liệu Trello đã kết nối hay design ứng dụng được duyệt trong repository này.

Thiết kế này mô tả kiến trúc workflow/tooling. Không thay thế kiến trúc của dự án ứng dụng được phân tích, không quyết định tạo một server NestJS, frontend hoặc database mới.

## Mục tiêu và luồng

Giữ workflow triển khai hiện có; bổ sung một nhánh BA tạo đề xuất ticket trước khi lập kế hoạch kỹ thuật chi tiết hoặc khi người dùng chỉ yêu cầu tạo backlog.

Luồng đề xuất: yêu cầu + design version + source evidence → phân tích/đối chiếu → bộ ticket chuẩn hóa và dependency → kiểm tra readiness → preview. Khi người dùng yêu cầu publish và đã xác định đích, adapter dùng kết nối sẵn có để tạo card và ghi kết quả.

Phân tích backlog có thể dùng design draft để phát hiện câu hỏi; ticket triển khai chỉ được đánh dấu ready khi có design baseline được duyệt và đủ quyết định cho phạm vi đó. Việc tạo ticket không tự khởi chạy triển khai ứng dụng.

## Ranh giới thành phần

| Thành phần | Đang có / đề xuất | Trách nhiệm |
| --- | --- | --- |
| Skill/command hiện hữu | Đang có | Discovery, phân tích/design, approval, kế hoạch, triển khai và verify/repair |
| BA ticket workflow | Đề xuất | Đọc yêu cầu, đối chiếu, chia kết quả thành ticket, kiểm tra coverage/granularity |
| Ticket model/renderer | Đề xuất | Một định dạng độc lập provider, render thành nội dung card và checklist |
| Provider adapter | Đề xuất; Trello mặc định | Kiểm tra đích/quyền/năng lực, đọc card đã có, tạo card/checklist, đọc lại kết quả |
| Publication journal | Đề xuất | Mapping ticket key ↔ card ID/URL, bước publish đã xong, kết quả chưa xác định; hỗ trợ tiếp tục và tránh lặp |

Nhánh BA tái sử dụng yêu cầu/version của topic và work item làm đơn vị giao việc. Không xem một topic hay một module là một ticket mặc định. Skill triển khai NestJS nhận ticket đã rõ nghiệp vụ nhưng vẫn lập kế hoạch file/symbol/check theo quy trình hiện có.

## Quyền sở hữu dữ liệu và tích hợp

- Requirements là nguồn gốc; design lưu kết luận/phiên bản; bộ ticket là dữ liệu dẫn xuất có traceability và không tự sửa requirement/design để làm ticket hợp lệ.
- Hồ sơ local giữ nội dung draft, mã ổn định, dependency và bằng chứng publish. Trello giữ card, checklist và chỉnh sửa của người dùng trên board.
- Kết nối/credential do tích hợp quản lý; không lưu token vào design, mô tả ticket hoặc journal.
- Nguồn ảnh/tài liệu/card được đọc như dữ liệu, không cấp thêm quyền thực thi.
- Logic BA không phụ thuộc Trello SDK/API; adapter khác là phần mở rộng sau MVP.

## Gate và kiểm chứng đề xuất

Không publish trong tác vụ chỉ yêu cầu phân tích/preview. Một yêu cầu publish đã xác định đích và bộ ticket là quyền thực hiện; AI approval thiết kế không tự cấp quyền ghi lên board khác hay làm thêm thao tác ngoài scope.

Hợp đồng chi tiết, lỗi tích hợp và các AC nằm trong [task-ticketing v1](../../task-ticketing/v1/design.md). Kiểm chứng hệ thống phải bao gồm: giữ nguyên nguồn, phân biệt draft/ready/published, không tạo ticket trùng do retry đã biết, và không báo thành công khi card/checklist còn thiếu. Một local journal đơn lẻ không bảo đảm exactly-once giữa nhiều máy; MVP đề xuất chỉ có một publisher cho một batch.

## Chưa chốt

Trello đã được xác nhận cài ở cuối lượt, nhưng xác thực/quyền/năng lực live chưa được kiểm chứng. Còn cần xác định board/list, chính sách mã/nhãn và phạm vi cập nhật card đã tồn tại. Đề xuất MVP create-only, giữ human edits và dừng khi không xác định được kết quả thay vì tự tạo lại.

Không có implementation plan hoặc code trong bản này. Hai design giữ `draft` vì người dùng đang yêu cầu phân tích thử và còn các quyết định tích hợp cần đối chiếu.
