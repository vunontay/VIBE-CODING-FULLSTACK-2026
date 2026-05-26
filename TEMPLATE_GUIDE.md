# Hướng Dẫn Template

Các template này sẵn sàng để bạn sao chép vào dự án của mình. Mỗi template phục vụ một mục đích cụ thể trong quy trình làm việc của agent. Hãy chỉnh sửa nội dung cho phù hợp với các lệnh, đường dẫn, tên tính năng và các bước xác minh của dự án bạn.

## Bắt Đầu Như Thế Nào

Trước tiên, hãy sao chép bốn tệp sau vào thư mục gốc của dự án:

1. `AGENTS.md` hoặc `CLAUDE.md`
2. `init.sh`
3. `claude-progress.md`
4. `feature_list.json`

Thêm các tệp còn lại khi dự án phát triển dần.

---

## AGENTS.md

Tệp hướng dẫn gốc. Đây là thứ đầu tiên agent đọc khi bắt đầu một phiên làm việc. Tệp này định nghĩa các quy tắc vận hành: cần làm gì trước khi viết code, cách làm việc, và cách kết thúc phiên.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Thay thế các bước trong quy trình khởi động bằng đường dẫn và lệnh thực tế của dự án
- Điều chỉnh các quy tắc làm việc cho phù hợp với quy ước của nhóm bạn
- Giữ nguyên phần "định nghĩa hoàn thành" — đây là phần quan trọng nhất

**Tác dụng đối với agent:**

- Yêu cầu agent đọc trạng thái tiến độ và tính năng trước khi bắt đầu làm việc
- Buộc agent chỉ làm một tính năng tại một thời điểm
- Yêu cầu có bằng chứng trước khi đánh dấu bất cứ thứ gì là hoàn thành
- Định nghĩa thế nào là một phiên kết thúc sạch sẽ

Dùng `AGENTS.md` cho Codex hoặc các agent khác. Dùng `CLAUDE.md` nếu bạn đang làm việc với Claude Code — cấu trúc giống nhau, chỉ khác định dạng phù hợp với phong cách hướng dẫn của Claude.

## init.sh

Script khởi động. Chạy cài đặt dependency, kiểm tra xác minh và in lệnh khởi chạy — tất cả trong một lần.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Chỉnh sửa ba biến sau ở đầu file:
  - `INSTALL_CMD` — lệnh cài đặt dependency (ví dụ: `npm install`, `pip install -r requirements.txt`)
  - `VERIFY_CMD` — lệnh xác minh cơ bản (ví dụ: `npm test`, `pytest`)
  - `START_CMD` — lệnh khởi động server phát triển (ví dụ: `npm run dev`)
- Cấp quyền thực thi: `chmod +x init.sh`

**Tác dụng:**

1. In ra thư mục hiện tại (để bạn xác nhận script đang chạy đúng chỗ)
2. Cài đặt các dependency
3. Chạy lệnh xác minh
4. In ra lệnh khởi chạy (hoặc thực thi luôn nếu đặt `RUN_START_COMMAND=1`)

Nếu bước xác minh thất bại, agent phải dừng lại và sửa lỗi nền tảng trước khi làm bất cứ điều gì khác.

## claude-progress.md

Nhật ký tiến độ. Mỗi phiên làm việc đều ghi vào tệp này, và mỗi phiên mới đều đọc nó trước tiên.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Điền thông tin dự án vào phần "Trạng Thái Đã Xác Minh Hiện Tại"
- Cập nhật bản ghi phiên sau mỗi lần làm việc

**Ý nghĩa từng trường:**

- **Trạng Thái Đã Xác Minh Hiện Tại** — nguồn sự thật duy nhất về tình trạng dự án
  - `Thư mục gốc repository` — nơi dự án tồn tại
  - `Đường dẫn khởi động chuẩn` — lệnh để chạy dự án
  - `Đường dẫn xác minh chuẩn` — lệnh để chạy kiểm thử
  - `Tính năng chưa hoàn thành ưu tiên cao nhất` — nội dung phiên tiếp theo cần làm
  - `Vấn đề đang chặn` — bất kỳ thứ gì đang bị tắc nghẽn
- **Bản Ghi Phiên** — một mục cho mỗi phiên làm việc
  - `Mục tiêu` — bạn dự định làm gì
  - `Đã hoàn thành` — những gì thực sự được làm xong
  - `Đã chạy xác minh` — các kiểm thử nào đã được thực thi
  - `Bằng chứng đã ghi` — bằng chứng nào đã được lưu lại
  - `Commit` — những gì đã được commit
  - `Rủi ro đã biết` — những gì có thể bị hỏng
  - `Hành động tốt nhất tiếp theo` — phiên tiếp theo nên bắt đầu từ đâu

## feature_list.json

Bộ theo dõi tính năng. Danh sách ở định dạng máy đọc được gồm mọi tính năng agent cần triển khai, kèm trạng thái, các bước xác minh và bằng chứng.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Thay thế các tính năng mẫu bằng tính năng thực tế của bạn
- Mỗi tính năng cần có:
  - `id` — định danh ngắn, duy nhất
  - `priority` — số nguyên, số càng nhỏ thì ưu tiên càng cao
  - `area` — phần nào của ứng dụng (ví dụ: "chat", "import", "search")
  - `title` — mô tả ngắn
  - `user_visible_behavior` — người dùng sẽ thấy gì khi tính năng hoạt động
  - `status` — một trong các giá trị: `not_started`, `in_progress`, `blocked`, `passing`
  - `verification` — hướng dẫn từng bước để xác nhận tính năng hoạt động
  - `evidence` — bằng chứng đã ghi lại rằng xác minh đã thành công (do agent điền vào)
  - `notes` — bất kỳ thông tin bổ sung nào

**Quy tắc trạng thái:**

- `not_started` — chưa được đụng đến
- `in_progress` — tính năng đang được làm (chỉ một tính năng tại một thời điểm)
- `blocked` — không thể tiếp tục do một vấn đề đã được ghi nhận
- `passing` — xác minh đã thành công và bằng chứng đã được ghi lại

Agent chỉ được có đúng một tính năng ở trạng thái `in_progress` tại bất kỳ thời điểm nào.

## session-handoff.md

Ghi chú bàn giao gọn giữa các phiên. Dùng tệp này khi một phiên kết thúc và bạn muốn phiên tiếp theo tiếp nối nhanh chóng.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Điền vào cuối mỗi phiên (hoặc để agent điền)

**Nội dung từng phần:**

- **Đã xác minh** — những gì được xác nhận đang hoạt động và xác minh nào đã được chạy
- **Thay đổi trong phiên này** — code hoặc hạ tầng nào đã thay đổi
- **Vẫn bị lỗi hoặc chưa xác minh** — các vấn đề đã biết và các khu vực rủi ro
- **Hành động tốt nhất tiếp theo** — phiên tiếp theo nên làm gì, và không được đụng vào đâu
- **Các lệnh** — lệnh khởi động, xác minh và gỡ lỗi để tham khảo nhanh

Tệp này không bắt buộc với các phiên nhỏ. Nó trở nên quan trọng khi phiên làm việc dài hoặc dự án có nhiều khu vực đang hoạt động song song.

## clean-state-checklist.md

Danh sách kiểm tra cần thực hiện trước khi kết thúc mỗi phiên. Đảm bảo repository ở trạng thái tốt để phiên tiếp theo có thể bắt đầu sạch sẽ.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Chạy qua danh sách trước khi đóng phiên
- Agent cũng nên kiểm tra các mục này như một phần quy trình kết thúc phiên

**Những gì nó kiểm tra:**

- Quy trình khởi động chuẩn vẫn hoạt động
- Lệnh xác minh chuẩn vẫn chạy được
- Nhật ký tiến độ đã được cập nhật
- Danh sách tính năng phản ánh đúng trạng thái thực tế (không có mục `passing` sai)
- Không có công việc làm dở nào bị bỏ lại mà không ghi chép
- Phiên tiếp theo có thể tiếp tục mà không cần sửa thủ công

## evaluator-rubric.md

Bảng chấm điểm để đánh giá chất lượng đầu ra của agent. Dùng sau một phiên hoặc tại các mốc quan trọng của dự án để đánh giá liệu công việc có đạt chuẩn không.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Sau một phiên (hoặc một loạt phiên), chấm điểm công việc của agent theo sáu tiêu chí
- Mỗi tiêu chí được chấm từ 0 đến 2

**Sáu tiêu chí:**

1. **Tính đúng đắn** — triển khai có khớp với hành vi mục tiêu không?
2. **Xác minh** — các kiểm tra bắt buộc có thực sự được chạy, có bằng chứng không?
3. **Kỷ luật phạm vi** — agent có bám sát tính năng đã chọn không?
4. **Độ tin cậy** — kết quả có tồn tại sau khi khởi động lại hoặc chạy lại không?
5. **Khả năng bảo trì** — code và tài liệu có đủ rõ ràng cho phiên tiếp theo không?
6. **Sẵn sàng bàn giao** — phiên mới có thể tiếp tục chỉ dựa trên các artifact trong repo không?

**Các kết luận có thể có:**

- Chấp nhận — đạt chuẩn
- Sửa lại — cần sửa trước khi chấp nhận
- Chặn — có vấn đề căn bản cần giải quyết trước

**Quan trọng: bộ đánh giá cần được tinh chỉnh.** Mặc định, các agent là những người tự đánh giá kém — chúng phát hiện ra vấn đề rồi lại tự thuyết phục mình rằng mọi thứ vẫn ổn. Bạn sẽ cần lặp lại:

1. Chạy bộ đánh giá trên một sprint đã hoàn thành.
2. So sánh điểm của nó với đánh giá của chính bạn.
3. Chỗ nào khác nhau, hãy làm cho tiêu chí rõ ràng hơn về điều kiện đạt/trượt.
4. Chạy lại và kiểm tra sự nhất quán.
5. Lặp lại cho đến khi bộ đánh giá liên tục khớp với nhận xét của con người.

Hãy lên kế hoạch cho 3–5 vòng tinh chỉnh. Ghi lại từng thay đổi để bạn có thể theo dõi điều gì đã cải thiện sự nhất quán.

## quality-document.md

Ảnh chụp nhanh chất lượng, chấm điểm từng miền sản phẩm và tầng kiến trúc trong dự án của bạn. Theo dõi sức khỏe codebase theo thời gian, không chỉ đầu ra của từng phiên riêng lẻ.

**Cách sử dụng:**

- Sao chép vào thư mục gốc của dự án
- Trước khi bắt đầu phiên: đọc để hiểu phần nào của codebase đang yếu nhất
- Sau một phiên: cập nhật điểm dựa trên những gì đã thay đổi
- Theo thời gian: so sánh các ảnh chụp nhanh để xem thay đổi harness nào thực sự cải thiện sức khỏe codebase

**Những gì nó chấm điểm:**

- **Miền sản phẩm** (ví dụ: import tài liệu, luồng Q&A, lập chỉ mục): mỗi miền được chấm điểm (A–D) theo trạng thái xác minh, khả năng agent đọc hiểu, độ ổn định kiểm thử và các lỗ hổng chính
- **Tầng kiến trúc** (ví dụ: tiến trình chính, preload, renderer, services): mỗi tầng được chấm điểm về việc tuân thủ ranh giới và khả năng agent đọc hiểu

**Tại sao nó quan trọng:**

Bảng đánh giá chấm điểm đầu ra của từng agent. Tài liệu chất lượng chấm điểm bản thân codebase. Chúng trả lời những câu hỏi khác nhau:

- Bảng đánh giá: "Agent có làm tốt trong phiên này không?"
- Tài liệu chất lượng: "Dự án đang ngày càng mạnh hơn hay yếu hơn theo thời gian?"

**Khi nào cần cập nhật:**

- Sau mỗi phiên làm việc đáng kể
- Trước khi so sánh benchmark
- Sau các bước dọn dẹp hoặc đơn giản hóa
- Khi đưa một agent hoặc model mới vào dự án

**Liên kết với việc đơn giản hóa harness:**

Tài liệu chất lượng cũng hỗ trợ việc đơn giản hóa harness. Mỗi thành phần harness mã hóa một giả định về điều model không thể làm. Khi model cải tiến, những giả định này trở nên lỗi thời. Để kiểm tra xem một thành phần có còn cần thiết không:

1. Chụp ảnh nhanh tài liệu chất lượng.
2. Gỡ bỏ một thành phần harness.
3. Chạy bộ nhiệm vụ benchmark.
4. Chụp ảnh nhanh lần nữa.
5. So sánh — nếu điểm không giảm, thành phần đó là chi phí thừa. Nếu giảm, hãy khôi phục lại.
