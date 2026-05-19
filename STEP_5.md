Trong quy trình Vibe Coding Fullstack 2026, **Bước 5: AIDD (AI-Driven Development)** là giai đoạn thực thi mã nguồn hàng loạt dựa trên các "đường ray" đã thiết lập ở các bước trước. Đây là thời điểm vai trò của bạn chuyển dịch hoàn toàn từ người viết code sang **"Tổng biên tập" (Editor-in-Chief)**, tập trung vào điều phối và kiểm chứng logic.

Dưới đây là tài liệu chi tiết cách triển khai Bước 5:

### 1. Triết lý thực hiện: Kỷ nguyên Điều phối (Orchestration)
Kỹ năng quan trọng nhất năm 2026 không còn là thuộc lòng cú pháp mà là khả năng **chia nhỏ bài toán** để các AI Agent xử lý chính xác nhất. Việc phát triển giờ đây dựa trên **vòng lặp hội thoại khép kín**: bạn nêu ý tưởng, AI thực thi, và cả hai cùng hợp tác. Với các dự án mới (greenfield), phương pháp này có thể tăng tốc độ phát triển lên **gấp 10 lần** hoặc hơn.

### 2. Các AI Agent và Công cụ thực thi cốt lõi
*   **IDE AI-Native:** **Cursor** và **Windsurf** là lựa chọn hàng đầu cho việc lập trình ngôn ngữ tự nhiên, hỗ trợ chạy các agent chạy nền trên các nhánh công việc song song (parallel worktrees),,.
*   **Agent cấp hệ thống:** **Claude Code** hoặc **Devin** có khả năng tự động tạo khung (scaffold) toàn bộ dự án và phân chia nhiệm vụ cho các sub-agent làm việc trên từng file riêng biệt,.
*   **Giao thức ngữ cảnh:** Sử dụng **MCP (Model Context Protocol)** để AI có thể truy cập trực tiếp vào database, tài liệu và mã nguồn hiện tại nhằm tăng độ chính xác,.

### 3. Quy trình triển khai AIDD chi tiết

#### A. Tạo Scaffold nhanh (Xương sườn dự án)
*   **Hành động:** Để AI tự động thiết lập cấu trúc thư mục, cài đặt dependencies và cấu hình routing/state.
*   **Lợi ích:** Bạn chỉ cần phê duyệt (approve) mà không cần gõ tay, giúp tiết kiệm thời gian khởi tạo.

#### B. Phát triển theo nguyên tắc "1 Prompt = 1 Tính năng nhỏ"
*   **Hành động:** Chia lộ trình thành các tác vụ cực nhỏ (ví dụ: "thêm form đăng nhập", "tạo API endpoint GET /users").
*   **Kỹ thuật:** Sử dụng phím tắt **Cmd+K** để tạo mã và **Cmd+L** để chat trực tiếp với AI về logic. Đừng bao giờ yêu cầu AI "làm toàn bộ app" vì dễ tạo ra mã nguồn rác hoặc lỗi kiến trúc,.

#### C. Tận dụng Prompt-Architecture Coupling
*   **Lưu ý:** Độ chi tiết của prompt sẽ quyết định độ phức tạp của hạ tầng được sinh ra,. Ví dụ, yêu cầu trả về dữ liệu JSON có cấu trúc (Variant B) sẽ khiến AI tự thêm các bộ xác thực (Zod) và xử lý lỗi (Retry), làm tăng số dòng code lên gấp nhiều lần so với yêu cầu văn bản thuần túy,,.

#### D. Cam kết Git (Commit) liên tục
*   **Hành động:** Lập tức commit Git mỗi khi AI hoàn thành một chức năng nhỏ.
*   **Lý do:** AI đôi khi có thể chỉnh sửa hàng loạt file hoặc gây lỗi hệ thống bất ngờ; việc commit thường xuyên tạo ra các "điểm khôi phục" an toàn,.

### 4. Kiểm soát chất lượng & Mô hình Hybrid
Nghiên cứu cho thấy AI có thể khiến các lập trình viên kinh nghiệm chậm đi 19% trên các codebase cũ do phải tốn thời gian sửa các lỗi "gần đúng". Do đó, cần áp dụng **mô hình Hybrid**:
*   **Vibe Coding (70-90%):** Dùng cho các tính năng tiêu chuẩn, CRUD, dashboard và prototype,.
*   **Traditional Coding:** Tự tay viết các phần **Critical Path** như xác thực (Auth), thanh toán, mã hóa dữ liệu và các thuật toán hiệu năng cao,,.
*   **Review:** Mọi dòng code AI tạo ra phải được con người đọc qua ít nhất một lần để đảm bảo không có lỗ hổng bảo mật sơ đẳng (như OWASP Top 10),,.

### 5. Kết quả đầu ra (Deliverables)
1.  **Mã nguồn hoàn chỉnh:** Đã bao gồm cả Frontend và Backend chạy tốt trên môi trường phát triển (như **ServBay**),.
2.  **Nhật ký quyết định:** Trích xuất các lựa chọn kiến trúc từ dấu vết suy luận của AI để lưu thành tài liệu ADRs.
3.  **Hệ thống Unit Tests:** Đã pass toàn bộ các rào chắn đã thiết lập ở Bước 4.
