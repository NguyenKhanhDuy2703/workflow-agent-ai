# Ví dụ phân rã ticket — BA → Trello

Status: illustrative draft. Source: [original request](../../../requirements/task-ticketing/v1/request.md), proposed [design v1](design.md). Đây là ví dụ backlog ở mức kết quả, không phải implementation plan đã được phép thực hiện. Mã `DEMO-*` chỉ để tham chiếu trong ví dụ; chưa phải card ID trên Trello.

## Ví dụ nên tránh

Quá lớn: “Làm module BA và tích hợp Trello”. Không có một kết quả nhỏ để nghiệm thu, khó thấy tiến độ từng năng lực.

Quá vụn: “Tạo DTO”, “Tạo controller”, “Tạo service”, “Viết unit test” thành bốn card cho cùng một thao tác. Những bước này thường thuộc checklist của một ticket hành vi.

## Batch đề xuất cho chính yêu cầu hiện tại

Epic minh họa: BA phân tích và đưa backlog lên Trello. Tất cả ticket còn draft; priority, assignee, deadline và estimate chưa chốt. Mỗi ticket phải có kiểm chứng riêng; ticket batch cuối không thay test của các ticket trước.

| Key | Tiêu đề theo kết quả | Đầu ra/AC chính | Dependency thực tế |
| --- | --- | --- | --- |
| DEMO-01 | Đối chiếu yêu cầu với design và báo phần thiếu/mâu thuẫn | Mỗi requirement có nguồn, design version/section, các lớp evidence riêng và BA disposition; không nhầm covered với implemented | Không có |
| DEMO-02 | Đề xuất ticket nhỏ có kết quả và dependency rõ | Batch có goal/scope/AC/key ổn định; lý do split/merge; không chia riêng DTO/controller/service của cùng kết quả | Output DEMO-01 |
| DEMO-03 | Phát hiện ticket chưa sẵn sàng hoặc chồng lặp trước khi publish | Báo thiếu AC/nguồn, scope quá lớn/vụn, overlap, dependency vòng/thiếu và unknown metadata; không tự vá nghiệp vụ | Output DEMO-02 |
| DEMO-04 | Xem trước card và checklist theo mẫu tiếng Việt | Render mục tiêu/phạm vi/công việc/AC/nguồn/phụ thuộc; bỏ metadata chưa xác định; không external write | Hợp đồng batch từ DEMO-02; hiển thị findings DEMO-03 khi có |
| DEMO-05 | Chọn và kiểm tra đúng board/list Trello đích | Resolve đích và label/member mapping khi dùng; báo thiếu quyền/năng lực; không chọn list gần giống theo suy đoán | Kết nối Trello và định danh đích được cung cấp; có thể độc lập với nhánh BA |
| DEMO-06 | Tạo một card đủ nội dung và checklist rồi trả link xác minh | Tạo một ticket ready đã được yêu cầu publish; persist key/mapping, kiểm tra card đã có, đọc lại nội dung/checklist và trả trạng thái đúng | DEMO-03, DEMO-04, DEMO-05 |
| DEMO-07 | Tiếp tục publish bị gián đoạn mà không tạo lại card đã biết | Chịu được timeout và card-created/checklist-failed; reconcile/read-back; unknown/conflict không blind-create; giữ human edits | Năng lực tạo/đọc và journal từ DEMO-06 |
| DEMO-08 | Xuất bản batch có phụ thuộc và báo kết quả từng ticket | Giữ key/link dependency; xử lý card cũ đã liên kết; partial batch không báo all-success; chạy luồng BA → preview → publish → resume | DEMO-01 đến DEMO-07; không được xem DEMO-06 đơn lẻ là MVP batch hoàn chỉnh |

DEMO-06 và DEMO-07 tách theo use case thành công và tiếp tục phiên gián đoạn vì có trạng thái/bằng chứng riêng. Cả hai đều bắt buộc cho MVP publish thật; không coi lỗi retry là công việc tùy chọn để làm sau khi đã bàn giao.

## Một ticket minh họa đầy đủ

### [DEMO-01] Đối chiếu yêu cầu với design và chỉ rõ phần thiếu/mâu thuẫn

Epic/topic: BA → ticket / task-ticketing.

Loại: feature. Readiness: draft (design system/topic chưa approved).

Ưu tiên: chưa xác định. Ước lượng: chưa ước lượng, vì chưa chốt cách đóng gói công cụ và nguồn tài liệu thực tế. Kế hoạch/assignee: chưa xác định. Phụ thuộc: không có ticket trước; cần request và design root/version hoặc xác nhận tài liệu chưa tồn tại.

Nguồn: REQ-02, REQ-03 trong [design v1](design.md); [yêu cầu gốc](../../../requirements/task-ticketing/v1/request.md).

**Mục tiêu**

BA nhìn được mỗi yêu cầu đã được design định nghĩa tới đâu, code/ticket có bằng chứng gì và cần làm rõ hay tạo việc mới, trước khi chia ticket triển khai.

**Phạm vi**

Nhận yêu cầu và tài liệu đã chỉ định, trích requirement ID, chọn đúng design version và tạo ma trận đối chiếu. Code/card là bằng chứng bổ sung khi có quyền truy cập.

**Ngoài phạm vi**

Không sửa design/source, không tự quyết business rule còn thiếu, không publish hoặc cập nhật card, không mặc định project_education thiếu chức năng.

**Việc cần làm**

- Xác định nguồn request và topic/version; phân biệt design draft với approved.
- Liệt kê requirement/actor/observable outcome có nguồn.
- Đối chiếu requirement với section/decision/AC tương ứng trong design.
- Ghi riêng design coverage, code evidence và existing work; unknown phải giữ nguyên.
- Đề xuất reuse/change/new/spike/clarify/no-action có lý do, kèm câu hỏi cần trả lời.

**File/tài liệu liên quan để đối chiếu**

- Các thủ tục hiện có: `.agents/commands/extract-requirements.md`, `read-design.md`, `report-gaps.md`.
- Hợp đồng BA/ticket đề xuất: `design/docs/task-ticketing/v1/design.md`.
- Requirement/design/source của dự án mục tiêu sẽ được chọn lúc chạy thật. Đây không phải danh sách file code cần sửa.

**Tiêu chí nghiệm thu**

- AC-D01-1: Với mỗi requirement được trích xuất, có đúng định danh ổn định, nguồn và dòng đối chiếu; không bỏ im lặng requirement chưa hiểu.
- AC-D01-2: Có thể trình bày các trường hợp covered/partial/missing/conflict với section làm căn cứ; nguồn chưa truy cập ghi unknown ở lớp evidence phù hợp.
- AC-D01-3: Requirement đã có design nhưng chưa có code không bị đánh dấu “đã hoàn thành”; code quan sát được không tự chứng minh test đã pass.
- AC-D01-4: Khi design draft hoặc mâu thuẫn nghiệp vụ, output ghi blocker/câu hỏi; không đưa ticket phụ thuộc sang implementation-ready.
- AC-D01-5: Khi đã liên kết một card xử lý cùng requirement, output thể hiện reuse/delta có lý do, không tự đề xuất một bản sao toàn bộ.
- AC-D01-6: Quá trình chỉ đọc nguồn và xuất bản phân tích local, không có external write.

**Cách kiểm chứng đề xuất**

Bộ tài liệu fixture có requirement được bao phủ, thiếu một phần, mâu thuẫn, design draft, code chưa truy cập và card đã liên kết. Kiểm tra output truy xuất nguồn và trạng thái tương ứng; không cần kết nối board để chứng minh phân tích fixture. Luồng đọc board thật là kiểm tra tích hợp riêng khi có kết nối.

Workflow ticket key minh họa: `demo/task-ticketing/requirements-design-comparison`.

## Nhận xét ticket trong ảnh

Card `[CE-005]` có một câu hỏi nghiên cứu tương đối tập trung và các mục tiêu/công việc/file/đầu ra rõ hơn một card “làm module editor”. Không cần tách mỗi browser thành một card chỉ vì có nhiều browser.

Phần cần bổ sung nếu dùng làm ticket thực thi: tiêu chí tương thích cụ thể, cách đo bundle và ngưỡng/quy tắc đánh giá, dữ liệu ghi nhận lỗi IME, môi trường Safari sẵn có, và câu hỏi/giới hạn timebox được thống nhất. Kết luận phải phân biệt đạt/không đạt/chưa kiểm chứng, không chỉ “đã test”. Đây là nhận xét từ ảnh, không phải xác nhận thư viện hoặc phiên bản đó hoạt động và cũng không áp dụng deadline/P0 trong ảnh cho batch này.
