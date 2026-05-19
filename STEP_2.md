Trong quy trình Vibe Coding 2026, **Bước 2: SDD (Spec-Driven Development)** là giai đoạn chuyển hóa những mô tả ý tưởng thuần túy thành các đặc tả kỹ thuật và quy tắc (rules) chặt chẽ. Đây là lớp "quản trị" quan trọng nhằm ngăn chặn tình trạng AI tự ý đưa ra các quyết định kiến trúc sai lầm mà không có sự kiểm soát của con người (vibe architecting).

Dưới đây là tài liệu chi tiết về cách triển khai Bước 2:

### 1. Triết lý thực hiện: Prompt là Đặc tả Kiến trúc
Trong kỷ nguyên AI-native, các lựa chọn trong câu lệnh (prompt) chính là các quyết định kiến trúc. Việc khai báo các khả năng của AI (như truy cập công cụ) hoặc yêu cầu định dạng đầu ra (như JSON) sẽ trực tiếp xác định hạ tầng cần thiết của hệ thống. Do đó, SDD yêu cầu lập trình viên phải chủ động thiết lập "đường ray" cho AI trước khi bắt đầu viết code.

### 2. Các công cụ thiết lập Quy tắc (Guardrails)
Bạn cần sử dụng các tệp cấu hình chuyên dụng để "dạy" AI về tiêu chuẩn kỹ thuật của dự án:
*   **`.cursorrules` (Cursor):** Chứa các chỉ dẫn cụ thể để AI luôn tuân thủ phong cách viết code, kiến trúc thư mục và các thư viện ưu tiên của dự án.
*   **Memory Bank (Windsurf):** Lưu trữ ngữ cảnh dài hạn về các tiêu chuẩn thiết kế và kiến trúc của dự án, giúp AI "suy nghĩ" nhất quán qua nhiều phiên làm việc.
*   **`AGENTS.md`:** Một quy ước tiêu chuẩn hóa để định nghĩa vai trò, quyền hạn và giao thức tích hợp cho các AI agent tham gia vào dự án.
*   **Claude Code Hooks:** Cho phép thiết lập các điểm chặn để kiểm tra hoặc thực thi các tác vụ tự động khi AI thực hiện thay đổi.

### 3. Quy trình triển khai chi tiết
#### A. Thiết lập Kiến trúc chuẩn (Ví dụ: Hexagonal Architecture)
*   **Hành động:** Sử dụng AI để soạn thảo các quy tắc ép AI phải gen code theo từng layer của kiến trúc Hexagonal (Domain, Application, Infrastructure).
*   **Mục tiêu:** Đảm bảo code sạch, tách biệt hoàn toàn logic nghiệp vụ với các yếu tố hạ tầng như database hay UI, giúp hệ thống dễ bảo trì và mở rộng.

#### B. Định nghĩa "Prompt-Architecture Coupling"
Cần xác định rõ các thành phần hạ tầng sẽ xuất hiện dựa trên độ chi tiết của đặc tả:
*   **Nếu yêu cầu Output có cấu trúc (JSON):** Hệ thống sẽ tự động thêm các bộ parser, schema validator (như Zod) và trình xử lý lỗi.
*   **Nếu yêu cầu gọi hàm (Function Calling):** AI sẽ thiết lập thêm bộ định tuyến công cụ (Tool Router), trình thực thi và kho lưu trữ trạng thái.

#### C. Nhúng tiêu chuẩn Bảo mật vào Đặc tả
*   **Hành động:** Đưa các yêu cầu kiểm soát quyền truy cập và tiêu chuẩn an toàn (OWASP Top 10, MITRE) trực tiếp vào các chỉ dẫn hệ thống (system prompts).
*   **Lợi ích:** Giảm thiểu rủi ro bảo mật (hiện có 45% mã AI tạo ra chứa lỗ hổng) ngay từ khâu phác thảo, tránh việc phải "vá lỗi" tốn kém về sau.

### 4. Kết quả đầu ra (Deliverables)
*   **Tài liệu yêu cầu kỹ thuật (TRD):** Bản thiết kế giải pháp kỹ thuật, phân tích ưu nhược điểm của tech stack đã chọn và sơ đồ cơ sở dữ liệu.
*   **Hệ thống tệp quy tắc:** `.cursorrules`, `AGENTS.md`, hoặc cấu hình Memory Bank đã được thiết lập xong.
*   **Hồ sơ quyết định kiến trúc (ADRs):** Ghi lại các lý do AI hoặc con người chọn một công nghệ hay cấu trúc cụ thể để phục vụ việc kiểm soát sau này.

### 5. Lưu ý quan trọng
*   **Kiểm soát Conformance Layer:** So sánh biểu đồ phụ thuộc của mã được AI tạo ra với các ràng buộc đã thiết lập (ví dụ: "không thêm database mới mà không qua review") để phát hiện vi phạm sớm.
*   **Tránh nợ kỹ thuật:** Nếu không có quy tắc rõ ràng, AI sẽ mặc định theo các dữ liệu đào tạo cũ (priors), dễ dẫn đến kiến trúc "mì ăn liền" khó mở rộng.
