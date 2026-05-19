Trong quy trình Vibe Coding 2026, **Bước 3: UDD (UI-Driven Development)** là giai đoạn hiện thực hóa các ý tưởng từ Bước 1 và 2 thành giao diện người dùng, từ đó làm căn cứ để AI suy luận và xây dựng hệ thống Backend (API, Database) tương ứng.

Dưới đây là tài liệu hướng dẫn triển khai chi tiết cho Bước 3:

### 1. Triết lý thực hiện: Màn hình là Đặc tả (UI as Spec)
Thay vì bắt đầu từ cơ sở dữ liệu, bạn lấy trải nghiệm người dùng làm trung tâm. Khi AI hiểu được các thành phần trên màn hình (input, list, button), nó sẽ tự động xác định được các hợp đồng dữ liệu (data contracts) cần thiết để hỗ trợ giao diện đó. Điều này giúp giảm thiểu việc sửa đi sửa lại do sai lệch giữa Frontend và Backend.

### 2. Quy trình triển khai chi tiết

#### A. Tạo Prototype và UI Code nhanh (Scaffolding)
*   **Hành động:** Sử dụng các công cụ AI chuyên biệt để biến mô tả hoặc thiết kế thành mã nguồn giao diện.
*   **Công cụ:** 
    *   **v0 (Vercel), Bolt.new, Lovable:** Đây là những công cụ hàng đầu năm 2026 giúp tạo nhanh các ứng dụng full-stack hoặc thành phần UI từ ngôn ngữ tự nhiên.
    *   **Figma to Code (via MCP):** Sử dụng giao thức **Model Context Protocol (MCP)** để kết nối trực tiếp thiết kế từ Figma vào Cursor/Windsurf. Độ chính xác hiện tại đạt khoảng **60%**, đủ để AI bắt đầu xây dựng logic.
*   **Prompt mẫu:** *"Dựa trên PRD ở Bước 1, hãy tạo giao diện trang quản lý bookmark với danh sách hiển thị tag, thanh tìm kiếm và nút thêm mới sử dụng Tailwind CSS."*.

#### B. Suy diễn API từ Tương tác UI (API Inference)
*   **Hành động:** Từ các thành phần giao diện đã có, yêu cầu AI định nghĩa các điểm cuối (endpoints) để kết nối dữ liệu.
*   **Cách làm:** Đừng nói mơ hồ, hãy chỉ định cụ thể các phương thức:
    *   Ví dụ: *"Từ danh sách bookmark này, hãy thiết kế API RESTful: `GET /api/v1/bookmarks` để lấy dữ liệu và `POST /api/v1/bookmarks` để thêm mới kèm theo validation cho trường URL"*.
*   **Lợi ích:** AI sẽ tự động tạo ra các hàm `fetch` hoặc `axios` đồng bộ hoàn toàn với cấu trúc dữ liệu trên UI.

#### C. Thiết lập Hợp đồng dữ liệu (Data Contracts)
*   **Hành động:** Sử dụng các thư viện như **Zod** để định nghĩa schema dựa trên các trường thông tin hiển thị trên màn hình.
*   **Nguyên tắc:** UI yêu cầu gì, Schema phải có cái đó. Một UI cụ thể sẽ buộc hệ thống phải sinh ra các bộ xử lý lỗi (retry handlers) và trình xác thực (validators) tương ứng.

### 3. Bộ công cụ hỗ trợ UDD
| Loại công cụ | Tên đề xuất | Vai trò |
| :--- | :--- | :--- |
| **UI Generator** | v0, Bolt.new, Lovable | Tạo nhanh prototype và mã nguồn React/Tailwind. |
| **Thiết kế sang Code** | Figma to Code (MCP) | Chuyển đổi trực tiếp từ bản vẽ sang cấu trúc component. |
| **Xác thực dữ liệu** | Zod | Tạo schema dựa trên cấu trúc form/input của UI. |
| **Phát triển Full-stack** | Cursor, Windsurf | Thực thi logic kết nối Frontend và Backend. |

### 4. Kết quả đầu ra (Deliverables)
1.  **Mã nguồn Frontend:** Các component UI đã được phong cách hóa (styled) và có sẵn logic tương tác cơ bản.
2.  **Định nghĩa API (Swagger/Postman):** Danh sách các endpoint cần xây dựng ở bước tiếp theo.
3.  **Schema dữ liệu:** Cấu trúc JSON hoặc Zod schema định hình cách dữ liệu luân chuyển giữa các lớp.

### 5. Lưu ý để hiệu quả và tiết kiệm (Save Cost)
*   **Nguyên tắc "1 Prompt = 1 Tính năng nhỏ":** Đừng yêu cầu AI làm toàn bộ UI phức tạp trong một lần. Hãy làm từng phần (ví dụ: Header -> Sidebar -> Content List) để tránh AI tạo mã lỗi hoặc lãng phí token.
*   **Kiểm tra tính năng ngay:** Mở tệp `index.html` hoặc chạy dev server ngay sau khi AI sinh code để đảm bảo giao diện đúng "vibe" trước khi đi sâu vào logic Backend.
*   **Tận dụng CRUD:** Các ứng dụng CRUD truyền thống là thế mạnh tuyệt đối của Vibe Coding, giúp tăng tốc độ lên gấp **10 lần** so với lập trình thủ công.
