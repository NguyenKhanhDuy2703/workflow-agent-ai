# Gaps và câu hỏi: task-ticketing v1

Status: draft, analysis only. Sources: [request](../../../requirements/task-ticketing/v1/request.md), [design](design.md), discovery/plugin lookup in this chat.

## Đã kiểm tra

- Tất cả skill/command hiện có liên quan đến requirement/design/plan đã được đọc. Chưa có executable ticket publisher hay ticketing skill mới.
- Tích hợp Trello ban đầu chưa cài; lần kiểm tra cuối lượt xác nhận đã cài. Chưa xác minh trạng thái xác thực, quyền board hoặc tập thao tác read/write thực tế; không thực hiện thao tác Trello live trong lượt này.
- Đã đọc ảnh đính kèm. Ảnh không chứa board/list ID/URL đủ để định danh đích publish.
- Không có design đã duyệt hoặc source tool trong repo. System/topic được lưu draft; chưa có application source để so sánh chức năng tool, vì thế source comparison ghi “no application source exists”. Các procedure hiện hữu chỉ là nguồn về workflow.

## Cần quyết định trước khi đóng thiết kế/triển khai phần tương ứng

| Gap | Vì sao cần | Chặn phần nào | Quyết định/đầu vào cần |
| --- | --- | --- | --- |
| Cách dùng công cụ | Chưa rõ chỉ dùng trong chat/skill hay còn cần CLI/service độc lập | Đóng hợp đồng thực thi/persistence và chọn implementation stages | Đề xuất bắt đầu bằng skill/command + kết nối sẵn có; xác nhận có cần executable riêng không |
| Nguồn chạy thử nghiệp vụ | Lần này chỉ có yêu cầu công cụ và mẫu card, không có feature bundle mới | Phân tích và tạo backlog thật cho một feature | Chọn một request cụ thể và design root/version của dự án mục tiêu |
| Năng lực/kết nối Trello | Đã cài không chứng minh đã truy cập board hoặc có đủ checklist/read-back operations | Kiểm chứng/publish thật; không chặn local BA preview | Xác minh kết nối/quyền/capability thực tế; chỉ cần kết nối thêm nếu trạng thái xác thực chưa hoàn tất; đánh giá REST/helper nếu thiếu |
| Board/list và quyền | Không có đích đáng tin cậy trong ảnh | External write | Board/list URL hoặc ID; kiểm tra có quyền với đúng đích |
| Quy ước metadata | Không nên tự suy prefix/epic/priority/member/deadline | Mapping những trường được dùng | Prefix mã, cách map epic/labels, assignee/date nếu có; đề xuất để trống khi chưa biết |

## Đề xuất không chặn phân tích

- Một ticket một kết quả kiểm chứng được, checklist giữ các bước DTO/controller/service/test của cùng hành vi.
- Mục tiêu ước lượng 0,5–2 ngày công là gợi ý cần hiệu chỉnh theo nhóm; chưa dùng như hard limit hoặc deadline.
- Preview trước external write trong tác vụ phân tích; publish khi có yêu cầu rõ về batch/đích, không thêm vòng xin phép lặp nếu đã được ủy quyền.
- MVP create-only, stable keys + journal/read-back/resume; không overwrite card người dùng đã sửa, không tự chuyển Done.
- Batch demo dùng chính yêu cầu BA → Trello; không thực hiện tính năng Fabric/React trong ảnh hoặc tạo việc trùng những chức năng đã có trong project_education.

## Điểm dừng và bước tiếp theo

Lượt này hoàn thành phân tích thử, tài liệu draft và ticket mẫu; không triển khai tool hoặc tạo card. Có thể tiếp tục hiệu chỉnh/duyệt thiết kế sau khi các quyết định cần cho phạm vi thực hiện được làm rõ. `plan-implementation` chỉ chạy trên exact system/topic versions đã approved; live publishing còn cần đích, kết nối và ủy quyền thích hợp.
