Trong quy trình Vibe Coding Fullstack 2026, **Bước 4: TDD (Test-Driven Development)** không chỉ đơn thuần là tìm lỗi, mà đóng vai trò là "bản đặc tả sống" và lớp rào chắn bảo mật cốt lõi để kiểm soát mã nguồn do AI tạo ra. Do khoảng **45% mã do AI sinh ra hiện nay vẫn chứa các lỗ hổng bảo mật kinh điển** (như OWASP Top 10), việc triển khai TDD là bắt buộc để chuyển từ lập trình cảm tính sang kỹ thuật tự trị chuyên nghiệp.

Dưới đây là chi tiết triển khai Bước 4:

### 1. Xây dựng Bộ Test làm Tài liệu Đặc tả (TDD as Living Spec)
Thay vì viết code chức năng trước, bạn yêu cầu AI dựa trên tài liệu SDD và UDD đã có để tạo bộ khung kiểm thử.
*   **AI-Generated Testing:** Tận dụng khả năng của AI trong việc tạo ra các trường hợp kiểm thử (test cases), bao gồm cả các trường hợp biên (edge cases) mà con người thường bỏ sót.
*   **Cấu trúc Unit & Integration Test:** Yêu cầu AI viết test cho các logic nghiệp vụ quan trọng và các điểm kết nối API đã định nghĩa ở Bước 3.
*   **Prompt thực thi:** *"Dựa trên file `AGENTS.md` và API spec, hãy viết bộ Unit Test sử dụng Vitest cho tính năng thêm bookmark, đảm bảo bao phủ các trường hợp URL không hợp lệ và tag trống"*.

### 2. Thiết lập Rào chắn Bảo mật & Kiểm soát (Security Guardrails)
Mã nguồn AI thường thiếu cơ chế xác thực và bảo mật lõi nếu không được nhắc nhở.
*   **Nhúng tiêu chuẩn vào System Prompts:** Các yêu cầu kiểm soát quyền truy cập và tiêu chuẩn an toàn (như **OWASP, MITRE**) phải được nhúng trực tiếp vào các tệp quy tắc như `.cursorrules` hoặc tệp hướng dẫn hệ thống của AI.
*   **Xác thực đầu ra có cấu trúc (Structured Output Validation):** Sử dụng các thư viện như **Zod** để ép AI phải tuân thủ hợp đồng dữ liệu. Việc này tạo ra một "lớp bảo chứng" (conformance layer) giúp hệ thống tự động từ chối các phản hồi không đúng cấu trúc hoặc có nguy cơ gây lỗi.
*   **Xử lý lỗi và Retry:** Thiết lập sẵn các bộ xử lý lỗi (error handlers), logic thử lại (retry) và trình tạo dữ liệu dự phòng (fallback) để tăng độ ổn định cho hệ thống.

### 3. Mô hình "Kỹ thuật tự trị" (Agentic Engineering Audit)
Đây là kỹ thuật tiên tiến nhất năm 2026 để đảm bảo an toàn dữ liệu doanh nghiệp.
*   **Cơ chế đánh giá chéo:** Thiết lập quy trình nơi **một AI Agent viết mã và một AI Agent khác thực hiện rà soát lỗ hổng**. 
*   **Kiểm thử tự động SAST/DAST:** Tích hợp các công cụ kiểm thử bảo mật mã nguồn tĩnh (SAST) và động (DAST) vào quy trình triển khai để đánh chặn mọi nỗ lực khai thác lỗ hổng từ mã nguồn AI ngay khi chúng vừa được sinh ra.

### 4. Công cụ và Tài liệu đầu ra (Deliverables)
*   **Công cụ:** Sử dụng **Cursor/Windsurf Rules** để hướng dẫn AI suy nghĩ (thinking) và kiểm lỗi; tích hợp các công cụ quét lỗ hổng (Vulnerability Scan).
*   **Kết quả đầu ra:**
    1.  **Bộ mã nguồn Test:** Đã bao phủ các luồng logic quan trọng.
    2.  **Báo cáo tuân thủ (Conformance Report):** So sánh đồ thị phụ thuộc của mã AI tạo ra với các ràng buộc kiến trúc đã thiết lập.
    3.  **Hồ sơ quyết định kiến trúc (ADR):** Ghi lại lý do AI hoặc con người chọn các phương thức bảo mật cụ thể.

### 5. Lưu ý quan trọng
*   **Sự hoài nghi cần thiết:** Mọi đoạn mã do AI sinh ra phải được đối xử với sự hoài nghi tương đương mã do lập trình viên thực tập viết; bắt buộc phải được đánh giá chéo.
*   **Giám sát 24/7:** Đối với các hệ thống production, cần có sự giám sát liên tục từ các trung tâm điều hành an ninh mạng (SOC) để kiểm soát toàn diện mọi truy cập.
