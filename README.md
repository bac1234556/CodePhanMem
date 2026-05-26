
# student-mentor-matching-system

# Hệ Thống Kết Nối Học Tập Và Định Hướng Nghề Nghiệp Mentor Hub

> Hệ thống kết nối cố vấn học tập theo thời gian thực, tích hợp trợ lý trí tuệ nhân tạo AI RAG và quy trình tự động hóa DevOps, được xây dựng theo kiến trúc Modular Monolith kết hợp AI Microservice độc lập.

---

## 1. Mô Tả Tổng Quan Dự Án

Hệ thống **Mentor Hub** là một nền tảng công nghệ số toàn diện nhằm giải quyết các bài toán khó, hỗ trợ ôn thi cấp tốc và định hướng lộ trình nghề nghiệp cá nhân hóa cho sinh viên. Hệ thống kết nối trực tiếp sinh viên (Mentee) với các cố vấn (Mentor) là những cựu sinh viên xuất sắc, thủ khoa hoặc chuyên gia đang đi làm.

Dự án tập trung vào ba trục công nghệ lõi:

* **Realtime**: Khớp lệnh tìm kiếm cố vấn, điều phối cuộc gọi hỗ trợ, trao đổi dữ liệu phòng học trực tuyến và trừ chi phí ví tài khoản theo thời gian thực nhờ công nghệ SignalR kết hợp WebRTC.
* **AI RAG**: Dịch vụ AI chuyên biệt sử dụng kỹ thuật Retrieval-Augmented Generation để tự động hóa việc hỏi đáp quy chế đào tạo, đề cương môn học, gợi ý lộ trình phát triển và kiểm duyệt hồ sơ năng lực đầu vào.
* **DevOps**: Đóng gói hoàn chỉnh bằng Docker Compose, thiết lập luồng tự động hóa kiểm thử và triển khai thông qua GitHub Actions, tích hợp giám sát Health Check hệ thống và thông báo trạng thái qua Telegram.

Dự án được chuẩn hóa theo quy trình phát triển phần mềm chuẩn doanh nghiệp, áp dụng nghiêm ngặt Git Workflow, quản lý tiến độ qua GitHub Issues/Projects, cam kết API Contract công khai và tài liệu hóa kiến trúc hệ thống chi tiết.

---

## 2. Mục Tiêu Chiến Lược Của Hệ Thống

Hệ thống hướng tới việc hiện thực hóa các mục tiêu sau:

* Số hóa và tối ưu hóa quy trình tìm kiếm gia sư, cố vấn học tập trong môi trường đại học.
* Cắt giảm tối đa thời gian chờ đợi của sinh viên khi gặp các nút thắt kiến thức trước kỳ thi nhờ mô hình On-demand (gọi là có ngay).
* Hỗ trợ các Mentor giỏi tăng thu nhập từ tri thức dựa trên cơ chế tính phí minh bạch theo phút (Pay-per-minute).
* Giúp Ban quản trị tự động hóa khâu kiểm duyệt hồ sơ Mentor thông qua AI, giảm tải nhân lực vận hành.
* Cung cấp cho người dùng một Trợ lý AI học tập đáng tin cậy, truy xuất có căn cứ từ kho tài liệu chuẩn của nhà trường, loại bỏ hoàn toàn hiện tượng AI bịa đặt thông tin (Hallucination).
* Chuẩn hóa hạ tầng DevOps để toàn bộ mã nguồn có thể xây dựng, kiểm thử tự động và triển khai lên môi trường máy chủ chỉ qua một click.

---

## 3. Phân Rã Chức Năng Nghiệp Vụ

### 3.1. Nhóm Chức Năng Cho Học Viên (Mentee)

* Khám phá danh mục môn học và cây kỹ năng chuyên ngành.
* Tìm kiếm nâng cao và lọc bộ lọc Mentor theo: chuyên môn, mức phí/phút, xếp hạng (số sao) và trạng thái hoạt động (Online/Offline).
* Xem chi tiết hồ sơ Mentor, bao gồm thành tích, bảng điểm minh chứng và các đánh giá từ học viên cũ.
* Đặt lịch hẹn cố vấn theo khung giờ hoặc sử dụng tính năng "Gọi ngay" để kết nối tức thì.
* Kết nối vào phòng học trực tuyến (Chat, Audio/Video Call, Chia sẻ màn hình).
* Nạp tiền vào ví điện tử hệ thống (giả lập qua các cổng thanh toán số).
* Theo dõi biến động số dư và chi phí lớp học hiển thị theo thời gian thực.
* Tương tác với Trợ lý AI để nhận tư vấn tài liệu và lộ trình tự học.

### 3.2. Nhóm Chức Năng Cho Cố Vấn (Mentor)

* Đăng ký tài khoản chuyên gia, cập nhật hồ sơ năng lực và tải lên minh chứng (CV, bằng cấp, bảng điểm).
* Thiết lập trạng thái biểu phí dịch vụ (Số tiền quy đổi trên mỗi phút hỗ trợ).
* Quản lý lịch trình rảnh rỗi để học viên chủ động đặt lịch trước.
* Sử dụng nút gạt trạng thái để sẵn sàng tiếp nhận cuộc gọi khẩn cấp (**Toggle Ready Status**).
* Nhận tín hiệu và âm thanh báo cuộc gọi đến theo thời gian thực để đưa ra quyết định Chấp nhận/Từ chối.
* Xem bảng điều khiển (Dashboard) thu nhập cá nhân: Tổng số phút đã kết nối, doanh thu tạm tính và số dư khả dụng có thể rút.

### 3.3. Chức Năng Quản Lý Phòng Học Trực Tuyến Realtime

* Tiếp nhận yêu cầu kết nối từ học viên và điều phối tín hiệu đến cố vấn phù hợp ngay lập tức.
* Khởi tạo phòng học ảo bảo mật dựa trên giao thức kết nối ngang hàng P2P (WebRTC).
* Quản lý các trạng thái của phiên học trực tuyến:
* Đang chờ kết nối (Pending)
* Đang kết nối (Connected)
* Mất tín hiệu tạm thời (Reconnecting)
* Đã kết thúc hoàn thành (Finished)


* Đồng bộ hóa bảng trắng (Whiteboard) hoặc khung chat nội bộ giữa hai bên.
* Đưa ra cảnh báo hệ thống hoặc tự động ngắt kết nối nếu tài khoản học viên hết số dư.

### 3.4. Chức Năng Ví Điện Tử & Thanh Toán Giao Dịch

* Quản lý số dư tài khoản của toàn bộ người dùng trong hệ thống dưới dạng ví điện tử (E-wallet).
* Khởi tạo yêu cầu nạp tiền thông qua việc sinh mã QR thanh toán động.
* Thực hiện cơ chế **Micro-billing**: Khấu trừ tiền tự động sau mỗi block thời gian (ví dụ: cứ mỗi 1 phút hệ thống sẽ quét số dư và thực hiện giao dịch tạm tính).
* Thực hiện quyết toán khi phiên học kết thúc: Khấu trừ tiền từ ví Mentee, thực hiện cắt chiết khấu sàn (ví dụ: 20%) và chuyển số tiền thực nhận còn lại vào ví Mentor.
* Quản lý lịch sử giao dịch và sao kê tài chính minh bạch cho từng tài khoản.

### 3.5. Chức Năng Dashboard Cho Ban Quản Trị (Admin)

* Xem bảng thống kê tổng quan về hiệu suất vận hành của toàn bộ nền tảng.
* Giám sát số lượng phiên học đang diễn ra trực tuyến theo thời gian thực.
* Kiểm duyệt danh sách hồ sơ đăng ký làm Mentor (Duyệt thủ công kết hợp với các gợi ý phân tích từ AI).
* Quản lý cấu trúc cây môn học, phân loại các khoa, viện của trường đại học.
* Theo dõi biểu đồ doanh thu chiết khấu hệ thống và số lượng giao dịch rút tiền của Mentor.
* Tiếp nhận và xử lý các khiếu nại về chất lượng ca học hoặc các hành vi gian lận tài chính.

### 3.6. Bộ Giải Pháp Trí Tuệ Nhân Tạo AI Services

* Trực tiếp trả lời các câu hỏi về đề cương chi tiết môn học, tài liệu tham khảo và quy chế học tập tại trường.
* Phân tích nhu cầu, mục tiêu đầu ra của sinh viên để thiết kế và sinh ra một lộ trình học tập, luyện thi cá nhân hóa.
* Hỗ trợ giải đáp các thắc mắc về chính sách vận hành, cơ chế nạp rút tiền và quy tắc ứng xử trên nền tảng.
* Tự động quét nội dung CV, bảng điểm đầu vào của Mentor để chấm điểm độ uy tín, phát hiện sai lệch và lập báo cáo thẩm định gửi về Admin.
* Đảm bảo toàn bộ câu trả lời được neo dữ liệu gốc từ Vector Database, loại bỏ hiện tượng sai lệch thông tin.

---

## 4. Thiết Kế Kiến Trúc Tổng Thể

Dự án áp dụng mô hình kiến trúc **Modular Monolith kết hợp AI Service riêng biệt**.

Phần Backend chính viết bằng C# .NET được chia nhỏ thành các module nghiệp vụ biệt lập về mặt logic. Cách thiết kế này giúp nhóm phát triển kiểm soát mã nguồn tốt, dễ dàng nâng cấp lên Microservices trong tương lai mà không làm phức tạp hóa hạ tầng ở giai đoạn đầu.

Khối AI Service do sử dụng hệ sinh thái Python nên được tách riêng thành một dịch vụ độc lập kết nối qua giao thức RESTful API.

```text
Client Applications (Giao Diện Người Dùng)
├── Mentee Web Client (Học viên)
└── Admin & Mentor Console (Cố vấn & Quản trị)
        |
        v
ASP.NET Core Backend - Modular Monolith (C#)
├── Identity Module (Định danh & Xác thực)
├── Profile Module (Hồ sơ & Minh chứng)
├── Session Module (Điều phối ca học & Lịch hẹn)
├── Wallet Module (Xử lý ví & Giao dịch thanh toán)
├── Notification Module (Hệ thống thông báo & Telegram Alert)
└── Admin Dashboard Module (Báo cáo & Kiểm duyệt)
        |
        ├── PostgreSQL (Cơ sở dữ liệu quan hệ)
        ├── Redis (Lưu trạng thái Online/Offline & Cache Session)
        └── SignalR Hub (Cổng truyền thông thời gian thực)
        |
        v
FastAPI AI RAG Service (Python)
├── Knowledge Base (Kho giáo trình, Quy chế, Đề cương)
├── Embedding Pipeline (Trích xuất đặc trưng)
├── Vector Store (ChromaDB / FAISS)
└── LLM Provider (Gemini API)

```

---

## 5. Stack Công Nghệ Lựa Chọn

### 5.1. Frontend (Giao Diện)

* Framework chính: React.js hoặc Next.js (bản 14+)
* Ngôn ngữ: TypeScript
* Thư viện CSS: Tailwind CSS kết hợp thư viện UI thành phần `shadcn/ui`
* Quản lý trạng thái server: TanStack Query (React Query)
* Quản lý trạng thái client: Zustand
* Biểu mẫu & Kiểm thử dữ liệu: React Hook Form tích hợp Zod Validation
* Kết nối thời gian thực: SignalR Client SDK
* Truyền tải âm thanh/hình ảnh: WebRTC API / Agora SDK

### 5.2. Backend (Máy Chủ Chính)

* Công nghệ cốt lõi: ASP.NET Core 8 / 9
* Kiến trúc truy cập dữ liệu: Entity Framework Core (Code First)
* Hệ quản trị cơ sở dữ liệu: PostgreSQL
* Xử lý Socket/Realtime: SignalR Hub
* Cơ chế bảo mật: JWT Authentication & Role-Based Authorization
* Kiểm định dữ liệu đầu vào: FluentValidation
* Ghi nhật ký hệ thống: Serilog xuất dữ liệu ra file và console
* Tài liệu hóa API: Swagger / OpenAPI Specification

### 5.3. AI Service (Trí Tuệ Nhân Tạo)

* Ngôn ngữ: Python 3.11+
* Web Framework: FastAPI
* Khai báo cấu trúc dữ liệu: Pydantic v2
* Thư viện điều phối RAG: LangChain hoặc LlamaIndex
* Cơ sở dữ liệu vector: ChromaDB hoặc FAISS
* Mô hình nhúng (Embedding): `text-embedding-004` (Google) hoặc tương đương
* Trí tuệ nhân tạo lõi: Gemini API (Mô hình `gemini-1.5-flash` / `gemini-1.5-pro`)

### 5.4. Vận Hành DevOps

* Công nghệ đóng gói: Docker & Docker Image Optimization
* Điều phối hạ tầng local: Docker Compose
* Hệ thống CI/CD: GitHub Actions Tự động hóa quy trình
* Máy chủ Proxy ngược: Nginx đảm nhận điều phối cổng và SSL
* Kiểm tra sức khỏe hệ thống: ASP.NET Core Health Checks
* Hệ thống thông báo khẩn cấp: Telegram Bot API tích hợp luồng Deploy/Error
* Tự động hóa sao lưu: Bash Script tự động backup định kỳ PostgreSQL

---

## 6. Tổ Chức Cấu Trúc Thư Mục Repository

```text
mentor-hub-system/
│
├── MentorHubSystem.sln
│
├── docs/
│   ├── agent-briefing.md
│   ├── architecture.md
│   ├── api-contract.md
│   ├── db-schema.md
│   ├── ui-flow.md
│   ├── git-workflow-guide.md
│   ├── demo-script.md
│   └── issue-template.md
│
├── backend/
│   └── mentor-api/
│       ├── src/
│       │   ├── MentorHub.Api/
│       │   ├── MentorHub.Application/
│       │   ├── MentorHub.Domain/
│       │   └── MentorHub.Infrastructure/
│       │
│       └── tests/
│           ├── MentorHub.UnitTests/
│           └── MentorHub.IntegrationTests/
│
├── frontend/
│   ├── mentee-web/
│   └── admin-mentor-web/
│
├── services/
│   └── ai-service/
│       ├── app/
│       ├── knowledge_base/
│       ├── requirements.txt
│       ├── Dockerfile
│       └── README.md
│
├── infrastructure/
│   ├── docker-compose.local.yml
│   ├── nginx/
│   └── scripts/
│
├── .github/
│   └── workflows/
│
├── .gitignore
└── README.md

```

---

## 7. Tổ Chức Các Module Ở Khối Backend

Mã nguồn Backend nằm gọn trong một ứng dụng ASP.NET Core nhưng phân chia cấu trúc thư mục nghiêm ngặt theo các Module nghiệp vụ độc lập:

```text
MentorHub.Api/
├── Modules/
│   ├── Identity/
│   ├── Profile/
│   ├── Session/
│   ├── Wallet/
│   ├── Notification/
│   └── Dashboard/
│
├── Shared/
│   ├── Auth/
│   ├── Database/
│   ├── Realtime/
│   ├── Exceptions/
│   └── Common/
│
├── Controllers/
├── Program.cs
└── appsettings.json

```

| Tên Module | Trách nhiệm xử lý chi tiết |
| --- | --- |
| **Identity** | Cấp phát khóa JWT, thiết lập xác thực, phân quyền Mentee/Mentor/Admin, đăng ký tài khoản. |
| **Profile** | Lưu trữ hồ sơ, quản lý cây kỹ năng/môn học, xử lý tệp tin đính kèm (bảng điểm, chứng chỉ). |
| **Session** | Điều phối lịch hẹn, tạo phòng học trực tuyến, xử lý logic trạng thái phòng học WebRTC. |
| **Wallet** | Quản lý ví điện tử, sinh mã nạp tiền, xử lý logic trừ tiền theo phút và chia sẻ doanh thu tự động. |
| **Notification** | Bắn thông báo đẩy (Push Notification) trên web và kích hoạt Bot Telegram báo động hệ thống. |
| **Dashboard** | Tổng hợp số liệu từ các module, tính toán biểu đồ doanh thu và cung cấp dữ liệu báo cáo cho Admin. |

---

## 8. Sơ Đồ Quy Trình Nghiệp Vụ Cốt Lõi

```text
Hệ thống nạp cấu trúc giáo trình & Admin phê duyệt cây môn học
        |
Mentor đăng ký, đẩy minh chứng năng lực -> AI quét & Admin duyệt hồ sơ
        |
Mentor gạt nút chuyển sang trạng thái "ONLINE" (Sẵn sàng tiếp nhận cuộc gọi)
        |
Mentee truy cập, tìm kiếm theo bộ lọc môn học -> Hệ thống hiển thị danh sách trực tuyến
        |
Mentee bấm nút "GỌI CỐ VẤN" -> Hệ thống kiểm tra số dư ví khả dụng
        |
Tín hiệu realtime được bắn qua SignalR -> Màn hình Mentor đổ chuông báo
        |
Mentor bấm "CHẤP NHẬN" -> Khởi tạo phòng WebRTC và kích hoạt bộ đếm thời gian
        |
Phiên học diễn ra -> Định kỳ mỗi phút hệ thống tạm tính tiền theo block thời gian
        |
Một trong hai bên cúp máy hoặc Mentee hết tiền -> Ngắt kết nối phòng học
        |
Hệ thống quyết toán hóa đơn: Trừ tiền ví Mentee -> Trích chiết khấu -> Cộng tiền ví Mentor
        |
Mentee chấm điểm đánh giá -> Quản lý vào xem Dashboard hiệu suất hệ thống
        |
Học viên đặt câu hỏi cho AI RAG để tự ôn tập kiến thức nền tảng

```

---

## 9. Cơ Chế Xử Lý Thời Thực (Realtime Design)

Tất cả các tương tác trực tiếp được thiết lập qua **SignalR Hub** nhằm đảm bảo độ trễ tối thiểu.

### 9.1. Các sự kiện truyền tải chính

```text
MentorOnlineStatusChanged  // Thông báo danh sách cố vấn vừa cập nhật trạng thái hoạt động
IncomingCallReceived      // Gửi tín hiệu đổ chuông và thông tin cuộc gọi đến cho Mentor
CallRequestRejected        // Thông báo cho Mentee biết Mentor đã từ chối hoặc bận máy
CallSessionEstablished     // Kích hoạt kết nối thành công, bắt đầu đồng bộ hóa luồng WebRTC
BillingTickProcessed      // Gửi thông báo cập nhật số tiền hiện tại và thời gian đã trôi qua theo từng phút
CallSessionTerminated      // Đồng bộ ngắt kết nối khi kết thúc phiên học
WalletBalanceUpdated       // Cập nhật biến động số dư tức thời trên màn hình người dùng

```

### 9.2. Kịch bản kiểm thử realtime

* **Kịch bản 1**: Mentor bấm bật Online, lập tức trên màn hình tìm kiếm của Mentee, thẻ hồ sơ của Mentor chuyển từ xám sang xanh sáng mà không cần tải lại trang.
* **Kịch bản 2**: Mentee bấm gọi, màn hình Mentor lập tức xuất hiện Pop-up đổ chuông đi kèm hiệu ứng âm thanh thời gian thực. Nếu quá 30 giây không phản hồi, hệ thống tự động hủy cuộc gọi.
* **Kịch bản 3**: Trong lúc ca học đang diễn ra, đồng hồ đếm ngược chạy đồng thời với việc số dư tài khoản của Mentee giảm dần sau mỗi phút, hiển thị trực quan lên giao diện.

---

## 10. Giải Pháp Trí Tuệ Nhân Tạo AI RAG Pipeline

Khối dịch vụ AI Service chạy độc lập dưới dạng một REST API gọn nhẹ cấu hình bằng FastAPI.

### 10.1. Kho tri thức nguồn (Knowledge Base)

```text
services/ai-service/knowledge_base/
├── quy_che_dao_tao_tin_chi.md   // Các quy định về học vụ, điểm số, điều kiện cảnh cáo, tốt nghiệp
├── de_cuong_lap_trinh_csharp.md // Chi tiết môn học C#, cấu trúc đề thi, các chương mục trọng tâm
├── tai_lieu_xac_suat_thong_ke.md// Đề cương và các dạng bài tập toán xác suất thống kê mẫu
├── chính_sach_mentor_hub.md     // Quy định về tỷ lệ chiết khấu tài chính, quy tắc ứng xử sàn
└── cau_hoi_thuong_gap_faq.md    // Tổng hợp các thắc mắc phổ biến của sinh viên

```

### 10.2. Mô Hình Luồng Xử Lý RAG

```text
Sinh viên gửi câu hỏi cần tư vấn lộ trình học hoặc ôn thi
→ FastAPI tiếp nhận Payload yêu cầu
→ Gọi mô hình nhúng tạo Vector Embedding cho câu hỏi đầu vào
→ Thực hiện tìm kiếm tương đồng ngữ nghĩa (Similarity Search) trên ChromaDB / FAISS
→ Trích xuất ra các đoạn văn bản (Chunks) chứa tri thức liên quan nhất từ file tài liệu (.md)
→ Đóng gói Context (Bối cảnh trích xuất) + Câu hỏi gốc vào một System Prompt mẫu
→ Đẩy Prompt sang Gemini API để xử lý sinh văn bản
→ Gemini trả ra câu trả lời chuẩn xác, có trích dẫn nguồn dữ liệu thực tế
→ FastAPI trả kết quả định dạng JSON về giao diện Client

```

### 10.3. Thiết Kế Danh Sách API AI

```text
POST /api/v1/ai/academy-consultant // Trực tiếp tư vấn giải đáp kiến thức môn học và ôn thi cho Mentee
POST /api/v1/ai/career-pathfinder  // Tiếp nhận mục tiêu để sinh ra lộ trình học tập cá nhân hóa
POST /api/v1/ai/cv-screening       // Phân tích cấu trúc CV, bảng điểm Mentor phục vụ cho khâu kiểm duyệt của Admin
POST /api/v1/ai/vector-reindex     // Lệnh từ Admin yêu cầu quét lại kho tri thức khi có tài liệu mới cập nhật
GET  /health                       // Endpoint kiểm tra trạng thái sống của dịch vụ AI

```

---

## 11. Chiến Lược Vận Hành DevOps & Triển Khai

### 11.1. Các thành phần hạ tầng

* **Docker hóa**: Toàn bộ hệ thống được chia làm 4 container chính: `mentor-backend-api`, `mentor-ai-service`, `mentee-frontend`, `admin-mentor-frontend`.
* **Hạ tầng bổ trợ**: Sử dụng các Container chính hãng được cấu hình sẵn cho `postgres:16-alpine` và `redis:7-alpine`.
* **Nginx Proxy**: Đứng ở cổng ngoài chịu trách nhiệm phân định luồng: các request bắt đầu bằng `/api` hướng về phía Backend, `/ai` hướng về Python Service, còn lại điều hướng về các nhánh Frontend tương ứng.

### 11.2. Quy trình tích hợp liên tục CI

```text
Thành viên tạo Pull Request (PR) đi vào nhánh 'develop'
→ Kích hoạt GitHub Actions Runner
→ Thực hiện khôi phục gói (Nuget Restore / Pip Install / Npm Install)
→ Thực hiện Build kiểm tra lỗi cú pháp trên toàn bộ các project
→ Khởi chạy toàn bộ hệ thống Unit Test và Integration Test ở Backend
→ Thực hiện Linting kiểm tra chuẩn định dạng mã nguồn Python
→ Nếu tất cả các bước trả về mã màu xanh (Pass) -> Cho phép Reviewer bấm Merge code

```

### 11.3. Quy trình triển khai liên tục CD

```text
Khi code được hợp nhất thành công vào nhánh chính 'main'
→ GitHub Actions kích hoạt tiến trình đóng gói Docker Image
→ Đẩy các Image đã được gắn thẻ phiên bản lên Docker Hub (hoặc GitHub Packages)
→ Kết nối tự động tới máy chủ VPS thông qua giao thức bảo mật SSH
→ Di chuyển vào thư mục hạ tầng và thực hiện lệnh: docker compose pull && docker compose up -d
→ Chạy lệnh script tự động kiểm tra endpoint /health của Backend và AI Service
→ Nếu hệ thống sống khỏe, kích hoạt Webhook gửi tin nhắn chúc mừng triển khai thành công về nhóm Telegram

```

---

## 12. Hướng Dẫn Thiết Lập Môi Trường Phát Triển Local

### 12.1. Công Cụ Bắt Buộc

* Hệ thống quản lý mã nguồn: **Git**
* Môi trường ảo hóa: **Docker Desktop** (Đã tích hợp sẵn Docker Compose)
* Bộ phát triển phần mềm: **.NET SDK 8 / 9**
* Môi trường chạy NodeJS: **Node.js LTS**
* Ngôn ngữ lập trình: **Python 3.11 hoặc cao hơn**
* Trình biên dịch khuyên dùng: **Visual Studio 2022** hoặc **VS Code**

### 12.2. Tải Mã Nguồn

```bash
git clone https://github.com/<owner>/mentor-hub-system.git
cd mentor-hub-system

```

### 12.3. Khởi Chạy Hạ Tầng Bổ Trợ

```bash
docker compose -f infrastructure/docker-compose.local.yml up -d
docker ps

```

Đảm bảo hai container sau đang chạy ổn định:

* `mentor-postgres` (Cổng 5432)
* `mentor-redis` (Cổng 6379)

### 12.4. Khởi Động Backend API

Mở tệp giải pháp bằng Visual Studio: `MentorHubSystem.sln` và chọn `MentorHub.Api` làm Startup Project rồi nhấn `F5`.

Hoặc thực thi thông qua giao diện dòng lệnh Terminal:

```bash
dotnet build MentorHubSystem.sln
dotnet run --project backend/mentor-api/src/MentorHub.Api/MentorHub.Api.csproj

```

### 12.5. Cài Đặt AI Service

```bash
cd services/ai-service
python -m venv .venv
# Kích hoạt môi trường ảo trên Windows:
.venv\Scripts\activate
# Kích hoạt trên MacOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000

```

### 12.6. Cấu Hình Các Nhánh Frontend

Khởi chạy Giao diện dành cho Học viên (Mentee):

```bash
cd frontend/mentee-web
npm install
npm run dev

```

Khởi chạy Giao diện dành cho Cố vấn và Quản trị viên (Admin & Mentor Dashboard):

```bash
cd frontend/admin-mentor-web
npm install
npm run dev

```

---

## 13. Danh Sách Quản Lý Biến Môi Trường (`.env`)

Tạo tệp cấu hình `.env` tại thư mục gốc dựa trên mẫu `.env.example` dưới đây:

```env
# Cấu hình kết nối cơ sở dữ liệu quan hệ PostgreSQL
POSTGRES_USER=mentor_admin
POSTGRES_PASSWORD=mentor_secure_pass_2026
POSTGRES_DB=mentor_hub_db
POSTGRES_PORT=5432

# Điểm neo cổng kết nối dịch vụ
BACKEND_PORT=5001
AI_SERVICE_PORT=8000

# Cấu hình bảo mật và khóa xác thực danh tính
JWT_SECRET=super-secret-key-for-mentor-hub-system-architecture-2026
JWT_EXPIRY_DAYS=7

# Khóa bảo mật kết nối dịch vụ trí tuệ nhân tạo lõi
GEMINI_API_KEY=AIzaSyYourActualGeminiKeyHere_To_Be_Changed

# Cấu hình cổng thông báo thông tin tự động qua Telegram Bot
TELEGRAM_BOT_TOKEN=123456789:ABCdefGhIJKlmNoPQRsTUVwxyZ
TELEGRAM_CHAT_ID=-987654321

```

*Tuyệt đối nghiêm cấm việc commit tệp tin chứa mật khẩu thực tế lên các kho lưu trữ mã nguồn chung.*

---

## 14. Mô Hình Quản Lý Nhánh Git Workflow

Dự án áp dụng mô hình phân nhánh chuẩn để quản lý tiến độ:

```text
main      -> Nhánh phân phối chính thức, chỉ chứa code đã đóng gói ổn định để đem đi demo
develop   -> Nhánh tích hợp trung tâm, nơi toàn bộ các tính năng mới được gom về để kiểm thử
feature/* -> Nhánh tính năng biệt lập, phân tách theo từng Issue cụ thể được giao cho thành viên

```

Quy trình phát triển một tính năng tiêu chuẩn:

```bash
git checkout develop
git pull origin develop
git checkout -b feature/issue-10-connect-signalr-hub

# Thực hiện viết code và chạy test kiểm thử tại môi trường máy cục bộ local

git add .
git commit -m "feat: triển khai kết nối hoàn chỉnh cổng tín hiệu SignalR Hub"
git push -u origin feature/issue-10-connect-signalr-hub

```

Tiến hành truy cập vào GitHub để khởi tạo một yêu cầu kéo mã (**Pull Request**):
`feature/issue-10-connect-signalr-hub` → `develop`

Sau khi toàn bộ mã nguồn trên `develop` hoạt động ổn định và bước vào giai đoạn kết thúc môn học:
`develop` → `main`

---

## 15. Tiêu Chuẩn Quản Lý Task Và Kiểm Duyệt Code

### 15.1. Định Nghĩa Issue

Mọi công việc trong dự án bắt buộc phải được mô tả thông qua hệ thống Issue trên GitHub. Mỗi Issue phải làm rõ các cấu phần:

* **Mục tiêu**: Mô tả ngắn gọn tính năng cần làm.
* **Phạm vi tác động**: Nêu rõ những thư mục, lớp dữ liệu hoặc module nào sẽ bị chỉnh sửa.
* **API Contract liên quan**: Định nghĩa rõ cấu trúc Request/Response nếu có làm việc với Endpoint mới.
* **Tiêu chí chấp nhận (Acceptance Criteria)**: Các bước cụ thể để kiểm tra xem tính năng đã chạy đúng yêu cầu chưa.
* **Định nghĩa hoàn thành (Definition of Done)**: Mã nguồn không lỗi cú pháp, đã chạy test local thành công, không chứa secret key và đã cập nhật tài liệu liên quan.

### 15.2. Quy trình tạo Pull Request

Khi lập trình viên hoàn thành một Issue, họ sẽ tạo một Pull Request gửi lên nhóm. Mẫu mô tả PR bắt buộc phải tuân thủ cấu trúc:

```markdown
## Tóm tắt nội dung thay đổi

## Khớp nối Issue liên quan
Closes #10

## Danh sách các chỉnh sửa cốt lõi
- Bổ sung cấu trúc lưu trữ Hub trong Shared/Realtime
- Thiết lập cấu hình CORS cho phép kết nối Socket từ Frontend

## Các bước thực hiện kiểm thử nghiệm thu (Cách test)

## Bảng kiểm tra điều kiện (Checklist)
- [ ] Code đã biên dịch thành công (Build Pass)
- [ ] Đã chạy qua các kịch bản kiểm thử (Test Pass)
- [ ] Không vô tình commit tệp cấu hình chứa mã mật khẩu thật
- [ ] Đã đồng bộ tài liệu kiến trúc API contract nếu có thay đổi cấu trúc dữ liệu

```

---

## 16. Kế Hoạch Khởi Tạo Các Khối Công Việc Ban Đầu (Issues)

Dưới đây là danh sách các Issue nền tảng cần được tạo lập ngay trên GitHub để phân chia cho **nhóm 5 thành viên**:

```text
[ARCH] Thiết lập cấu trúc tài liệu kiến trúc tổng thể, API Contract và sơ đồ thực thể DB ban đầu.
[DEVOPS] Khởi tạo tệp cấu hình Docker Compose thiết lập môi trường Postgres và Redis cho local.
[BE] Tạo giải pháp phần mềm (.sln) và cấu trúc các thư mục dự án theo mô hình Modular Monolith.
[BE] Thiết lập hệ thống định danh, phân quyền Identity Module và cấu hình cấp phát mã khóa JWT.
[BE] Thiết lập Entity Framework Core cấu hình ánh xạ dữ liệu xuống hệ thống PostgreSQL.
[FE] Khởi tạo cấu trúc dự án Mentee Web Client sử dụng Next.js và Tailwind CSS.
[FE] Khởi tạo cấu trúc dự án Admin & Mentor Console Dashboard sử dụng React.js.
[AI] Khởi tạo khung mã nguồn độc lập FastAPI AI Service và cấu hình các route cơ bản.
[AI] Xây dựng cấu trúc kho dữ liệu tri thức Knowledge Base và viết hàm nhúng dữ liệu đầu tiên.
[DOCS] Hoàn thiện chi tiết đặc tả thiết kế cấu trúc bảng dữ liệu (Database Schema) bản sơ thảo.

```

---

## 17. Kịch Bản Nghiệm Thu & Demo Sản Phẩm

### 17.1. Các bước thực hiện demo

1. Triển khai kích hoạt toàn bộ hệ thống bằng một câu lệnh duy nhất thông qua Docker Compose để chứng minh hạ tầng sạch.
2. Trình bày trang quản lý dự án trên GitHub hiển thị lịch sử phân chia Task minh bạch qua hệ thống Issues/Pull Requests.
3. Show kết quả tự động chạy kiểm thử thành công của luồng GitHub Actions CI.
4. Đăng nhập đồng thời 3 cửa sổ trình duyệt tương ứng với 3 vai trò: Học viên (Mentee), Cố vấn (Mentor) và Admin hệ thống.
5. Thực hiện quy trình Mentor đăng ký tài khoản, đăng tải bảng điểm và xem AI thực hiện quét phân tích hồ sơ tự động.
6. Admin phê duyệt tài khoản Mentor, Mentor thực hiện thiết lập biểu phí và bật nút sẵn sàng nhận cuộc gọi (Online).
7. Học viên tìm kiếm môn học, tìm thấy Mentor, thực hiện lệnh gọi trực tuyến thời gian thực.
8. Trình diễn màn hình đổ chuông, đồng ý kết nối và luồng đếm thời gian trừ tiền ví điện tử tự động sau mỗi block một phút.
9. Thực hiện ngắt cuộc gọi, show hóa đơn giao dịch tài chính vừa tạo lập.
10. Học viên đặt câu hỏi cho Trợ lý AI để truy xuất kiến thức môn học dựa trên tài liệu chuẩn đã nhúng sẵn.

### 17.2. Các điểm mấu chốt cần làm nổi bật

* Khả năng **tự động hóa và cô lập** các Module nghiệp vụ bên trong kiến trúc Backend Modular Monolith.
* Tốc độ truyền tải tín hiệu và **đồng bộ trạng thái cuộc gọi trực tuyến** không độ trễ nhờ SignalR.
* Sự chuẩn xác và **tính xác thực cao của câu trả lời từ AI RAG**, chứng minh không bị hiện tượng ảo tưởng thông tin nhờ có nguồn dữ liệu đối chiếu rõ ràng từ Vector Store.
* Tính chuyên nghiệp của quy trình làm việc nhóm thể hiện qua lịch sử Git gọn gàng và hệ thống kiểm tra tự động DevOps.

---

## 18. Lộ Trình Nâng Cấp Và Phát Triển Tương Lai

* Tách biệt hoàn toàn các Module có tần suất sử dụng cao (như Module Session và Module Wallet) thành các dịch vụ Microservices chạy độc lập khi quy mô người dùng tăng trưởng.
* Tích hợp thêm hệ thống xếp hàng tin nhắn **RabbitMQ** để xử lý các tác vụ bất đồng bộ nặng như gửi email biên lai, ghi log hệ thống hoặc đẩy thông tin phân tích lịch sử cuộc gọi.
* Triển khai chiến lược nâng cấp sản phẩm không gây gián đoạn hệ thống thông qua mô hình hình học **Blue/Green Deployment**.
* Bổ sung công cụ giám sát hiệu năng chuyên sâu sử dụng bộ công nghệ Prometheus kết hợp Grafana để vẽ biểu đồ tài nguyên máy chủ.
* Thực hiện kết nối trực tiếp với môi trường Sandbox của các cổng thanh toán thực tế phổ biến tại Việt Nam (MoMo, VNPAY).
* Xây dựng cơ chế đánh giá nâng cao (Advanced RAG Metrics) sử dụng khung kiểm thử Ragas để đo lường độ chính xác của câu trả lời từ trợ lý trí tuệ nhân tạo.

---

## 19. Văn Hóa Và Quy Tắc Phối Hợp Trong Đội Ngũ

Mọi thành viên trong dự án phải tuân thủ nghiêm ngặt quy trình vận hành khép kín dưới đây để đảm bảo chất lượng đồ án:

```text
Tiếp nhận Issue được giao 
→ Tự động tạo Branch cá nhân từ develop (feature/issue-*)
→ Thực hiện viết mã nguồn và chạy kiểm thử tại máy local 
→ Thực hiện Commit mã nguồn với cú pháp chuẩn (feat:, fix:, docs:)
→ Push nhánh lên kho lưu trữ chung trên GitHub 
→ Khởi tạo Pull Request (PR) 
→ Hệ thống GitHub Actions tự động kiểm tra điều kiện (CI)
→ Chỉ định ít nhất 1 thành viên khác trong nhóm vào thực hiện Code Review
→ Khắc phục các góp ý nếu có -> Tiến hành Merge code vào nhánh chung develop

```

**Các điều luật tối thượng của nhóm:**

* Nghiêm cấm mọi hành vi thực hiện commit chỉnh sửa mã nguồn trực tiếp trên hai nhánh cốt lõi là `main` và `develop`.
* Bất kỳ một sự thay đổi nào liên quan đến cấu trúc trả về của API bắt buộc phải thảo luận với nhóm và thực hiện cập nhật ngay vào tệp tài liệu contract `docs/api-contract.md`.
* Nếu có chỉnh sửa, thêm bớt các trường dữ liệu hoặc các bảng trong Database, lập tức phải cập nhật sơ đồ tại file `docs/db-schema.md`.
* Tuyệt đối không bao giờ được phép để lộ tệp cấu hình `.env` chứa mật khẩu thật lên Git. Mọi thông tin cấu hình mẫu chỉ được phép viết vào tệp `.env.example`.
* Mỗi Pull Request khi gửi đi bắt buộc phải ghi rõ kịch bản test và đính kèm hình ảnh hoặc video minh chứng tính năng đã chạy thành công tại máy cá nhân.

---

## 20. Tình Trạng Hiện Tại & Phạm Vi Nghiệm Thu

Kiến trúc mục tiêu tổng thể của đồ án:

```text
Modular Monolith C# Backend + FastAPI AI RAG Service + Realtime SignalR Hub + Dockerized DevOps Pipeline

```

Phạm vi các tính năng lõi bắt buộc phải hoàn thiện để phục vụ cho buổi báo cáo nghiệm thu trước hội đồng:

```text
- Chức năng đăng nhập, phân quyền người dùng và cấp phát JWT Token.
- Trang cá nhân của Mentor, chức năng tải minh chứng và nút gạt trạng thái Online/Offline.
- Hệ thống tìm kiếm, lọc danh sách Mentor trực tuyến dành cho Học viên.
- Luồng đổ chuông cuộc gọi trực tuyến thời gian thực sử dụng SignalR Hub.
- Trình mô phỏng tính phí theo phút (Micro-billing) và quyết toán ví điện tử khi cúp máy.
- Giao diện Dashboard thống kê biểu đồ doanh thu và quản lý duyệt hồ sơ dành cho Admin.
- Trợ lý học tập thông minh AI RAG thực hiện trả lời câu hỏi dựa trên tài liệu giáo trình chuẩn của nhà trường.
- Đóng gói toàn bộ mã nguồn chạy ổn định qua Docker Compose và luồng CI tự động của GitHub Actions.

```

---

## 21. Điều Khoản Sử Dụng & Bản Quyền (License)

Dự án này được nghiên cứu, thiết kế và phát triển hoàn toàn độc lập bởi các thành viên trong nhóm phục vụ cho mục đích học thuật, làm bài tập lớn và hoàn thành đồ án tốt nghiệp môn học tại nhà trường. Mọi hành vi sao chép, trích dẫn một phần hoặc toàn bộ cấu trúc tài liệu này vào các mục đích thương mại khác đều phải có sự đồng ý bằng văn bản của các thành viên trong nhóm sáng lập.
