# task-ticketing v1: BA phân tích và tạo ticket trên Trello

Status: draft. Approved by/date: unset. Date: 2026-11-06.

Sources: [yêu cầu gốc và ảnh](../../../requirements/task-ticketing/v1/request.md), [discovery](../../../discovery.md), [system v1 draft](../../system/v1/design.md), current workflow procedures. Đây là phân tích thử; chưa có skill/publisher mới, implementation plan hoặc card Trello được tạo.

## 1. Mục tiêu và yêu cầu truy xuất được

| ID | Yêu cầu đã có căn cứ | Nguồn |
| --- | --- | --- |
| REQ-01 | Bổ sung công cụ tạo task trên nền tảng quản lý task; Trello là mặc định | User request |
| REQ-02 | Làm việc theo vai trò BA để phân tích yêu cầu | User request |
| REQ-03 | Đối chiếu yêu cầu với tài liệu design trước khi đề xuất ticket | User request |
| REQ-04 | Chia ticket hợp lý, tránh một ticket quá lớn cho cả module | User request |
| REQ-05 | Trước mắt phân tích thử | User request |
| REF-01 | Tham khảo bố cục title/epic/priority/estimate/plan/dependencies/goal/work/files/done | Ảnh; đây là mẫu bố cục, không phải metadata bắt buộc của mọi ticket |

Các nội dung còn lại là đề xuất thiết kế của AI, không phải yêu cầu người dùng đã xác nhận.

## 2. Quy tắc BA và kích thước ticket đề xuất

Một ticket có một kết quả mà người nhận có thể triển khai và kiểm chứng với các đầu vào/phụ thuộc đã nêu. Epic/topic/module là nhóm công việc, không mặc định là một ticket.

Nguyên tắc chia:

- Chia theo hành vi/use case hoặc kết quả kỹ thuật độc lập, không theo tên module. Ví dụ tách tạo nhóm, thêm thành viên, gán gói quyền nếu mỗi việc có quy tắc/AC khác nhau.
- DTO, controller, service và test của cùng một hành vi thường là checklist trong cùng ticket. Không tạo mỗi HTTP status, mỗi file hoặc mỗi thao tác code thành một card.
- Tách backend, client hoặc migration chỉ khi có giao diện/handoff rõ, người nhận hoặc dependency thực tế khác, và mỗi phần có AC riêng. Ghi phụ thuộc khi một phần chưa chạy độc lập được.
- Tách theo tình huống/phạm vi khi một card chứa nhiều kết quả có thể nghiệm thu riêng, nhiều chủ thể/chính sách không liên quan, hoặc nhiều luồng dữ liệu độc lập.
- Đề xuất mục tiêu khoảng 0,5–2 ngày công nếu có cơ sở ước lượng. Vượt khoảng này là tín hiệu xem lại phạm vi, không tự động chia theo số file hay ép một ước lượng giả. Chính sách này chưa được người dùng chốt.
- Spike chỉ dùng để trả lời một câu hỏi còn bất định: ghi câu hỏi, phạm vi/timebox đề xuất, bằng chứng cần thu và quyết định đầu ra. Không dùng spike để che một feature chưa rõ phạm vi.
- Test cần để hoàn thành hành vi nằm trong ticket đó. Chỉ tách kiểm thử xuyên luồng khi có một kết quả tích hợp riêng; không dồn toàn bộ chất lượng vào ticket test cuối cùng.
- Không suy ra ngày bắt đầu/hạn giao, độ ưu tiên, assignee hoặc epic từ ảnh. Giá trị thiếu phải để trống/chưa xác định hoặc gắn nhãn AI đề xuất.

## 3. Luồng từ yêu cầu đến card

1. Nhận phạm vi và nguồn: request, tài liệu design/version, project/source root nếu có, work item liên quan, cấu hình provider. Với yêu cầu chỉ phân tích, chọn chế độ preview.
2. Trích xuất requirement ID, actor, goal, business rule, luồng thành công/thất bại và AC; lưu nguồn, đánh dấu câu hỏi/đề xuất.
3. Đối chiếu từng requirement với đúng design version và source/ticket đã có nếu truy cập được. Tách trạng thái tài liệu, bằng chứng code và card có sẵn; không coi chúng là cùng một loại coverage.
4. Đề xuất ticket theo kết quả, gộp/tách có lý do, liên kết requirement/AC và dependency. Nguồn chưa đủ cho triển khai thì giữ draft/needs-clarification hoặc đề xuất spike có mục tiêu rõ.
5. Kiểm tra batch: coverage, chồng lặp, độ lớn/độ vụn, AC, dependency cycle, nguồn và metadata chưa chốt. Trả preview và câu hỏi trước khi bất kỳ external write nào trong tác vụ phân tích.
6. Khi có yêu cầu publish xác định được bộ ticket và đích: kiểm tra kết nối, board/list, mapping và quyền/năng lực; đọc card đã có; chỉ chọn ticket đủ điều kiện.
7. Tạo card/checklist theo từng thao tác có journal; lưu card ID/URL, đọc lại kết quả, gắn tham chiếu dependency và trả báo cáo theo ticket. Không khởi chạy implementation từ hành động publish.

Việc yêu cầu tạo card cho batch/đích cụ thể có thể đã là ủy quyền publish; không bắt buộc hỏi xác nhận lại nếu đã rõ. AI approval design chỉ kiểm soát baseline, không tự cấp quyền ghi lên một board chưa được chỉ định.

## 4. Ma trận đối chiếu — không bỏ sót và không tạo trùng việc

Mỗi dòng ghi: requirement ID/nguồn → design topic/version/section/status → code evidence nếu có → existing ticket nếu có → quyết định BA → ticket/AC đề xuất.

| Loại đánh giá | Giá trị | Ý nghĩa |
| --- | --- | --- |
| Design coverage | covered / partial / missing / conflict | Design có định nghĩa đầy đủ hành vi được yêu cầu không? |
| Code evidence | observed / not-found / unknown | Đã thấy code liên quan hay chưa; static observation không chứng minh nó chạy đúng |
| Existing work | linked / not-found / unknown | Đã biết task/card tương ứng hay chưa; không truy cập board không đồng nghĩa không có card |
| BA disposition | reuse / change / new / spike / clarify / no-action | Đề xuất làm gì dựa trên ba lớp bằng chứng, kèm lý do |

Các trường hợp quan trọng:

- Design covered + chưa có implementation: vẫn có thể cần ticket triển khai mới; covered không đồng nghĩa đã làm.
- Code đã có hoặc card đã có: liên kết/reuse và kiểm tra phần delta; không tự sinh lại toàn bộ chức năng.
- Source chưa truy cập được: ghi unknown, không tuyên bố tính năng thiếu.
- Design draft: vẫn phân tích gap được, nhưng không đánh dấu ready cho ticket implementation dựa vào một baseline chưa được duyệt.
- Requirement mâu thuẫn design: ghi hai nguồn và tác động; không biến mâu thuẫn thành một ticket ready để người phát triển tự chọn nghiệp vụ.

## 5. Ticket chuẩn hóa và mức sẵn sàng

Hợp đồng đề xuất độc lập provider, chưa phải JSON schema hay executable helper đã triển khai.

| Nhóm | Trường và quy tắc |
| --- | --- |
| Identity | `ticketKey` ổn định trong namespace project/work item; tiêu đề thay đổi không đổi key; `batchId` và revision để truy xuất một lần chuẩn bị |
| Scope | title, kind (feature/bug/refactor/spike), goal, scope, exclusions, topic/epic và work item |
| Traceability | requirement IDs/sources, design topic/version/section/status, code evidence, existing-card references và AC IDs |
| Work | checklist công việc có ý nghĩa; file/module liên quan nếu đã có bằng chứng; không bịa đường dẫn hoặc endpoint |
| Acceptance | actor/preconditions/action/expected result; lỗi/denied/no-change khi liên quan; evidence cần có |
| Dependencies | ticket keys và loại quan hệ; input/output cần bàn giao; phân biệt thông tin liên quan với dependency thật |
| Planning | priority, estimate/rationale/confidence, assignee, start/due đều có thể chưa xác định; không suy due từ estimate |
| Readiness | draft / needs-clarification / ready; reasons và questions |
| Destination | provider mặc định Trello, board/list và mapping labels/members đã xác minh; tách khỏi nội dung BA |
| Publication | state riêng: not-started / publishing / partial / unknown / failed / published, card ID/URL và kết quả từng thao tác |

Readiness không phải tiến độ phát triển hay trạng thái design. `published` chỉ có nghĩa card đã được tạo/kiểm tra theo phạm vi publish; không có nghĩa task đã hoàn thành.

Một ticket implementation đạt ready khi có một kết quả rõ, AC đủ kiểm chứng, nguồn/design baseline được duyệt, dependency/handoff rõ, không có câu hỏi nghiệp vụ chặn và phạm vi hợp lý. Một spike có AC là bằng chứng/quyết định nghiên cứu, không phải cam kết feature đã xong. Các ticket mẫu của bản nháp này chưa phải ticket ready để triển khai.

## 6. Bố cục mô tả card

Theo ngôn ngữ dự án, mặc định đề xuất tiếng Việt: mã + tiêu đề; epic/topic; priority/estimate/plan nếu có; dependencies; nguồn yêu cầu/design; mục tiêu; phạm vi và ngoài phạm vi; việc cần làm; file/module liên quan; AC; cách kiểm chứng; câu hỏi/blocker; stable ticket key.

Checklist “Việc cần làm” và “Tiêu chí nghiệm thu” tách riêng nếu provider hỗ trợ. AC là kết quả cần đạt, không chỉ là “đã viết service/đã chạy test”. Không dùng link local `D:/...` như URL tài liệu truy cập được từ Trello; dùng URL repo/version đã xác minh hoặc ghi đường dẫn tương đối kèm version và giới hạn truy cập.

## 7. Ranh giới công cụ đề xuất

| Khả năng | Input → output | Giới hạn |
| --- | --- | --- |
| Analyze scope | Nguồn yêu cầu/design → requirement + comparison matrix + gaps | Read-only với nguồn nghiệp vụ |
| Decompose tickets | Matrix + mục tiêu → batch/ticket/AC/dependency | Không tự chốt nghiệp vụ còn thiếu |
| Review batch | Batch → coverage/split/merge/readiness findings | Không lấy số lượng card làm thước đo thành công |
| Preview | Batch → nội dung card/checklist và metadata thiếu | Không ghi Trello |
| Publish batch | Batch đủ điều kiện + đích/ủy quyền → kết quả per-ticket | Chỉ thao tác trong board/list/batch đã được chỉ định |
| Reconcile/resume | Journal + actual remote state → tiếp tục hoặc báo unknown/conflict | Không tạo lại khi chưa xác định thao tác trước có thành công không |

Ưu tiên triển khai dạng skill + command + hợp đồng ticket dùng kết nối sẵn có, phù hợp repository hiện tại. Chưa quyết định xây server NestJS hoặc CLI/script riêng. Nếu connector thiếu năng lực, đánh giá adapter REST/helper ở bước thiết kế bổ sung; không tuyên bố có tool thực thi khi mới có tài liệu.

## 8. Ánh xạ Trello và xử lý lỗi đề xuất

Theo [Cards API](https://developer.atlassian.com/cloud/trello/rest/api-group-cards/): `name` nhận tiêu đề, `desc` nhận mô tả, `idList` xác định list đích; labels/members dùng ID đã resolve; start/due chỉ gửi khi đã biết. Card trả về ID/URL để lưu mapping. Checklist và check item được tạo qua [Checklists API](https://developer.atlassian.com/cloud/trello/rest/api-group-checklists/).

Đây là mapping đề xuất dựa trên REST API, không phải xác nhận plugin có đủ thao tác đó. Khi kết nối phải kiểm tra năng lực thực tế. MVP không phụ thuộc Custom Fields/Power-Up hay native epic/dependency; đề xuất thể hiện epic bằng mapping nhãn/mô tả và phụ thuộc bằng key/link.

Chống trùng/tiếp tục:

- Persist stable ticket keys trước khi publish; gắn marker đọc được vào mô tả và journal card IDs/checklist IDs/các bước hoàn tất. Key không chỉ là tiêu đề hoặc index của batch.
- Đọc board đích và đối chiếu key, kể cả card đã archive khi cần; một match thì reuse/report, nhiều match thì conflict. Không truy cập đủ dữ liệu thì không tuyên bố dedup thành công.
- Nếu POST timeout, ghi unknown; tìm/read-back bằng marker hoặc mapping trước khi thử tạo lại. Không tìm ra ngay không chứng minh POST thất bại.
- Nếu card tạo thành công nhưng checklist lỗi, giữ mapping và báo partial; tiếp tục phần thiếu, không tạo card mới và không tự xóa card để rollback.
- Nếu journal/remote hoặc nội dung người dùng chỉnh khác bản trước, báo conflict. MVP create-only; không overwrite human edits hoặc tự cập nhật card cũ theo design mới.
- Một publisher cho một batch trong MVP; local lock/journal không bảo đảm exactly-once giữa nhiều máy. Khi có cạnh tranh hoặc kết quả mơ hồ, dừng phụ thuộc cần thiết để đối chiếu.
- Với throttling/lỗi tạm thời, dùng retry có giới hạn theo [rate-limit guidance](https://developer.atlassian.com/cloud/trello/guides/rest-api/rate-limits/), không retry vô hạn hoặc lặp create mù. Lỗi quyền/đích không được chữa bằng chọn board/list khác.
- Due có thời gian phải chuẩn hóa theo timezone được chỉ định (mặc định bối cảnh người dùng Asia/Saigon); không suy giờ từ ảnh. Không có deadline thì bỏ trường.

## 9. AC cho công cụ đề xuất

| AC | Kết quả kiểm chứng |
| --- | --- |
| AC-01 | Mỗi requirement đầu vào có dòng đối chiếu và ticket/decision hoặc câu hỏi cụ thể, không có requirement bị bỏ im lặng |
| AC-02 | Phân biệt coverage của design, bằng chứng code và existing ticket; unknown không bị biến thành missing |
| AC-03 | Ticket có kết quả/AC/handoff; phát hiện card gom cả module và card chỉ tách file/lớp mà không có kết quả riêng |
| AC-04 | Không xuất hiện priority/deadline/member hoặc business rule tự coi là user-confirmed; AI proposals có nhãn rõ |
| AC-05 | Dependency graph không có vòng; dependency ngoài batch phải có tham chiếu/handoff rõ |
| AC-06 | Preview hiển thị đầy đủ nội dung và readiness, không gọi external write; ticket dựa trên design chưa duyệt không thành implementation-ready |
| AC-07 | Publish đúng board/list đã xác minh, đúng nội dung đã chọn; lưu ID/URL và đọc lại card/checklist; không báo published khi còn thiếu phần bắt buộc |
| AC-08 | Chạy lại cùng ticket keys không tạo thêm card khi đã xác định card có sẵn; timeout/match mơ hồ trả unknown/conflict để đối chiếu |
| AC-09 | Lỗi sau tạo card giữ mapping và tiếp tục checklist thiếu, không tạo lại card; kết quả batch tách published/partial/failed/unknown |
| AC-10 | Chỉ cài/năng lực đã xác minh mới được coi là kết nối hoạt động; không ghi credential vào artifact/card/log |

Thiết kế và kiểm tra mẫu ở đây chưa chứng minh AC tích hợp đã chạy. Sau thiết kế được duyệt mới lập implementation plan và chọn harness/local fixtures/test board cho các kiểm tra cần external write.

## 10. Source comparison và gaps

Hiện có `extract-requirements`, `read-design`, `report-gaps`, `plan-change`, `manage-work-item` và profile NestJS. Chúng cung cấp đầu vào/truy xuất/gate, nhưng chưa có ticket decomposition, model/renderer, provider adapter hay publication journal thực thi. `plan-change` tạo kế hoạch kỹ thuật, không thay thế vai trò BA chia backlog.

Tích hợp Trello đã được xác nhận cài ở lần kiểm tra cuối lượt; xác thực/quyền và khả năng thao tác live chưa được kiểm chứng. Chưa có board/list hoặc business feature bundle để phân tích thật. Mẫu trong [examples.md](examples.md) sử dụng chính yêu cầu công cụ này để minh họa, không suy ra ứng dụng giáo dục đang thiếu tính năng.

Xem [open-questions.md](open-questions.md) để biết quyết định còn thiếu và phần bị chặn. Giữ status draft trong lượt phân tích thử này; không khởi chạy plan/implementation/publish.
