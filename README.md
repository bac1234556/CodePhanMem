# student-mentor-matching-system

# Hệ Thống Kết Nối Học Tập Và Định Hướng Nghề Nghiệp Mentor Hub

> Hệ thống kết nối cố vấn học tập theo thời gian thực, tích hợp trợ lý trí tuệ nhân tạo AI RAG và quy trình tự động hóa DevOps, được xây dựng theo kiến trúc Modular Monolith kết hợp AI Microservice độc lập.

---

## 1. Mô Tả Tổng Quan Dự Án

Hệ thống **Mentor Hub** là một nền tảng công nghệ số toàn diện nhằm giải quyết các bài toán khó, hỗ trợ ôn thi cấp tốc và định hướng lộ trình nghề nghiệp cá nhân hóa cho sinh viên. Hệ thống kết nối trực tiếp sinh viên ( với các cố vấn là những cựu sinh viên xuất sắc, thủ khoa hoặc chuyên gia đang đi làm.

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

### 3.1. Nhóm Chức Năng Cho Học Viên

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

### 3.5. Chức Năng Dashboard Cho Admin

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

Phần Backend chính được xây dựng bằng **Java (Spring Boot)** áp dụng cấu trúc **Multi-Module**, chia nhỏ các tầng và phân tách module nghiệp vụ một cách chặt chẽ về mặt logic. Thiết kế này hỗ trợ làm việc nhóm song song hiệu quả, dễ dàng nâng cấp lên Microservices trong tương lai mà không làm phức tạp hóa hạ tầng ở giai đoạn đầu.

Khối AI Service do sử dụng hệ sinh thái Python nên được tách riêng thành một dịch vụ độc lập kết nối qua giao thức RESTful API.

```text
Client Applications (Giao Diện Người Dùng)
├── Mentee Web Client (Học viên)
└── Admin & Mentor Console (Cố vấn & Quản trị)
        |
        v
Spring Boot Backend - Modular Monolith (Java Multi-Module)
├── mentor-web (REST Controllers, Security Config, WebSocket Endpoint)
├── mentor-application (Mục tiêu nghiệp vụ: Use Cases, DTOs, Services)
├── mentor-infrastructure (Hạ tầng: Spring Data JPA, Redis Cache, WebSocket Handler)
└── mentor-domain (Nghiệp vụ lõi: Entities, Value Objects, Domain Interfaces)
        |
        ├── PostgreSQL (Cơ sở dữ liệu quan hệ)
        ├── Redis (Lưu trạng thái Online/Offline & Cache Session cuộc gọi)
        └── Spring WebSocket / STOMP Hub (Cổng truyền thông thời gian thực)
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

### 5.1. Frontend

* Framework chính: React.js hoặc Next.js (bản 14+)
* Ngôn ngữ: TypeScript
* Thư viện CSS: Tailwind CSS kết hợp thư viện UI thành phần `shadcn/ui`
* Quản lý trạng thái server: TanStack Query (React Query)
* Quản lý trạng thái client: Zustand
* Biểu mẫu & Kiểm thử dữ liệu: React Hook Form tích hợp Zod Validation
* Kết nối thời gian thực: SockJS / STOMP Client (Giao tiếp với Spring WebSocket)
* Truyền tải âm thanh/hình ảnh: WebRTC API / Agora SDK

### 5.2. Backend

* Công nghệ cốt lõi: Java 17 hoặc Java 21 / Spring Boot 3.x
* Kiến trúc truy cập dữ liệu: Spring Data JPA (Hibernate) & Spring JDBC
* Hệ quản trị cơ sở dữ liệu: PostgreSQL
* Xử lý Socket/Realtime: Spring WebSocket (STOMP Protocol)
* Cơ chế bảo mật: Spring Security kết hợp JJWT (Java JWT) & Role-Based Authorization
* Kiểm định dữ liệu đầu vào: Jakarta Bean Validation (Hibernate Validator)
* Ghi nhật ký hệ thống: SLF4J & Logback
* Lập lịch tác vụ ngầm (Scheduler): Spring `@Scheduled` (Xử lý quét trừ tiền)
* Tài liệu hóa API: SpringDoc OpenAPI (Swagger UI)

### 5.3. AI Service

* Ngôn ngữ: Python 3.11+
* Web Framework: FastAPI
* Khai báo cấu trúc dữ liệu: Pydantic v2
* Thư viện điều phối RAG: LangChain hoặc LlamaIndex
* Cơ sở dữ liệu vector: ChromaDB hoặc FAISS
* Mô hình nhúng (Embedding): `text-embedding-004` (Google) hoặc tương đương
* Trí tuệ nhân tạo lõi: Gemini API (Mô hình `gemini-1.5-flash` / `gemini-1.5-pro`)

### 5.4. Vận Hành DevOps

* Công nghệ đóng gói: Docker & Jib (Tối ưu hóa Docker Image cho Java)
* Điều phối hạ tầng local: Docker Compose
* Hệ thống CI/CD: GitHub Actions Tự động hóa quy trình
* Máy chủ Proxy ngược: Nginx đảm nhận điều phối cổng và SSL
* Kiểm tra sức khỏe hệ thống: Spring Boot Actuator (`/actuator/health`)
* Hệ thống thông báo khẩn cấp: Telegram Bot API tích hợp luồng Deploy/Error
* Tự động hóa sao lưu: Bash Script tự động backup định kỳ PostgreSQL

---

## 6. Tổ Chức Cấu Trúc Thư Mục Repository

Sử dụng kiến trúc **Maven Multi-Module** giúp phân định ranh giới rõ ràng giữa các phần của hệ thống:

```text
mentor-hub-system/
│
├── docs/
│   ├── architecture.md
│   ├── api-contract.md
│   ├── db-schema.md
│   └── git-workflow-guide.md
│
├── backend/
│   └── mentor-api/
│       ├── pom.xml                        # Parent POM: Quản lý version thư viện chung
│       │
│       ├── mentor-domain/                 # Lớp thực thể và logic cốt lõi (Entities, Enums)
│       │   ├── src/main/java/vn/edu/cmc/mentorhub/domain/
│       │   └── pom.xml
│       │
│       ├── mentor-application/            # Lớp xử lý Use Cases, Business Logic
│       │   ├── src/main/java/vn/edu/cmc/mentorhub/application/
│       │   └── pom.xml
│       │
│       ├── mentor-infrastructure/         # Lớp kết nối DB (JPA), Cấu hình Redis, WebSocket
│       │   ├── src/main/java/vn/edu/cmc/mentorhub/infrastructure/
│       │   └── pom.xml
│       │
│       └── mentor-web/                    # Cổng tiếp nhận Request (Controllers, Security Filter)
│           ├── src/main/java/vn/edu/cmc/mentorhub/web/
│           ├── src/main/resources/        # application.yml
│           └── pom.xml
│
├── frontend/
│   ├── mentee-web/
│   └── admin-mentor-web/
│
├── services/
│   └── ai-service/
│
├── infrastructure/
│   ├── docker-compose.local.yml
│   └── nginx/
│
├── .github/
│   └── workflows/
│
├── .gitignore
└── README.md

```

---

## 7. Tổ Chức Các Module Gói Nghiệp Vụ Ở Khối Backend

Bên trong các module `mentor-application` và `mentor-infrastructure`, mã nguồn tiếp tục được phân tách nghiêm ngặt thành các package nghiệp vụ. Cách chia này cho phép một team 5 người có thể phân chia công việc độc lập, không bị chồng chéo code.

```text
vn.edu.cmc.mentorhub.application/
├── shared/                       # Các xử lý dùng chung (Exception, Utils, DTO nền)
├── identity/                     # Gói nghiệp vụ Định danh & Đăng ký tài khoản
├── profile/                      # Gói nghiệp vụ Hồ sơ Mentor, cây kỹ năng, bảng điểm
├── session/                      # Gói nghiệp vụ Lịch hẹn, Kết nối phòng học WebRTC
├── wallet/                       # Gói nghiệp vụ Ví điện tử, Micro-billing, Đối soát doanh thu
└── notification/                 # Gói nghiệp vụ Bắn thông báo qua Web và Telegram Bot

```
| Tên Package | Trách nhiệm xử lý chi tiết |
| --- | --- |
| **identity** | Xử lý Authentication (Spring Security), phân quyền Mentee/Mentor/Admin, cấp phát và xác thực JWT. |
| **profile** | Quản lý thông tin cá nhân, cây danh mục môn học, lưu trữ minh chứng năng lực (bằng cấp, bảng điểm). |
| **session** | Quản lý vòng đời ca học: Điều phối tín hiệu kết nối, xử lý logic trạng thái phòng học WebRTC (`PENDING`, `CONNECTED`, `FINISHED`). |
| **wallet** | Quản lý ví điện tử, xử lý trừ tiền tự động sử dụng `@Scheduled` (Micro-billing), tự động phân chia chiết khấu sàn và quyết toán thu nhập cho Mentor. |
| **notification** | Quản lý kênh truyền thông báo: Gửi tin nhắn real-time qua WebSocket STOMP và đẩy các cảnh báo về hệ thống Telegram Bot. |

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
Tín hiệu realtime được bắn qua Spring WebSocket -> Màn hình Mentor đổ chuông báo
        |
Mentor bấm "CHẤP NHẬN" -> Khởi tạo phòng WebRTC và kích hoạt bộ đếm thời gian
        |
Phiên học diễn ra -> Định kỳ mỗi phút Job Scheduler trừ tiền theo block thời gian
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

## 9. Cơ Chế Xử Lý Thời Thực

Tất cả các tương tác trực tiếp được thiết lập qua **Spring WebSocket (STOMP Protocol)** nhằm đảm bảo độ trễ tối thiểu và phản hồi ngay lập tức.

### 9.1. Các sự kiện truyền tải chính

```text
/topic/mentor-status     // Kênh Broadcast: Cập nhật danh sách cố vấn đang Online/Offline
/user/queue/calls        // Kênh Cá nhân: Gửi tín hiệu đổ chuông đến một Mentor cụ thể
/user/queue/call-replies // Kênh Cá nhân: Báo cho Mentee biết Mentor chấp nhận/từ chối
/topic/session/{id}      // Kênh Phòng học: Trao đổi SDP/ICE candidates cho WebRTC
/user/queue/billing      // Kênh Cá nhân: Gửi thông báo cập nhật số dư ví sau mỗi phút

```
### 9.2. Kịch bản kiểm thử realtime

* **Kịch bản 1**: Mentor bấm bật Online, lập tức trên màn hình tìm kiếm của Mentee, thẻ hồ sơ của Mentor chuyển từ xám sang xanh sáng mà không cần tải lại trang.
* **Kịch bản 2**: Mentee bấm gọi, màn hình Mentor lập tức xuất hiện Pop-up đổ chuông đi kèm hiệu ứng âm thanh. Nếu quá 30 giây không phản hồi, hệ thống tự động hủy cuộc gọi.
* **Kịch bản 3**: Trong lúc ca học đang diễn ra, đồng hồ đếm ngược chạy đồng thời với việc số dư tài khoản của Mentee giảm dần sau mỗi phút, hiển thị trực quan lên giao diện.

---

## 10. Giải Pháp Trí Tuệ Nhân Tạo AI RAG Pipeline

Khối dịch vụ AI Service chạy độc lập dưới dạng một REST API gọn nhẹ cấu hình bằng FastAPI (Python).

### 10.1. Kho tri thức nguồn

```text
services/ai-service/knowledge_base/
├── quy_che_dao_tao_tin_chi.md   // Các quy định về học vụ, điểm số, điều kiện tốt nghiệp
├── de_cuong_lap_trinh_java.md   // Chi tiết môn học Java Backend, cấu trúc đề thi
├── tai_lieu_xac_suat_thong_ke.md// Đề cương và các dạng bài tập toán xác suất thống kê mẫu
├── chính_sach_mentor_hub.md     // Quy định về tỷ lệ chiết khấu tài chính, quy tắc ứng xử
└── cau_hoi_thuong_gap_faq.md    // Tổng hợp các thắc mắc phổ biến của sinh viên

```

### 10.2. Mô Hình Luồng Xử Lý RAG

```text
Sinh viên gửi câu hỏi cần tư vấn lộ trình học hoặc ôn thi
→ FastAPI tiếp nhận Payload yêu cầu
→ Gọi mô hình nhúng tạo Vector Embedding cho câu hỏi đầu vào
→ Thực hiện tìm kiếm tương đồng (Similarity Search) trên ChromaDB / FAISS
→ Trích xuất ra các đoạn văn bản (Chunks) chứa tri thức liên quan nhất
→ Đóng gói Context (Bối cảnh trích xuất) + Câu hỏi gốc vào System Prompt
→ Đẩy Prompt sang Gemini API để xử lý sinh văn bản
→ Gemini trả ra câu trả lời chuẩn xác, có trích dẫn nguồn
→ FastAPI trả kết quả định dạng JSON về giao diện Client

```

### 10.3. Thiết Kế Danh Sách API AI

```text
POST /api/v1/ai/academy-consultant // Tư vấn giải đáp kiến thức môn học và ôn thi cho Mentee
POST /api/v1/ai/career-pathfinder  // Tiếp nhận mục tiêu sinh ra lộ trình học tập cá nhân hóa
POST /api/v1/ai/cv-screening       // Phân tích cấu trúc CV, bảng điểm Mentor phục vụ kiểm duyệt
POST /api/v1/ai/vector-reindex     // Admin yêu cầu quét lại kho tri thức khi có tài liệu mới
GET  /health                       // Endpoint kiểm tra trạng thái sống của dịch vụ AI

```

---

## 11. Chiến Lược Vận Hành DevOps & Triển Khai

### 11.1. Các thành phần hạ tầng
* **Docker hóa**: 4 container chính: `mentor-backend-api` (build qua Maven/Jib), `mentor-ai-service`, `mentee-frontend`, `admin-mentor-frontend`.
* **Hạ tầng bổ trợ**: Container `postgres:16-alpine` và `redis:7-alpine`.
* **Nginx Proxy**: Phân luồng các request `/api` về Java Backend, `/ai` về Python Service, còn lại hướng về các nhánh Frontend.

### 11.2. Quy trình tích hợp liên tục CI

```text
Thành viên tạo Pull Request (PR) đi vào nhánh 'develop'
→ Kích hoạt GitHub Actions Runner
→ Maven thực hiện tải dependency và Build toàn bộ Multi-module
→ Khởi chạy toàn bộ hệ thống Unit Test và Integration Test ở Backend (JUnit/Mockito)
→ Thực hiện Linting kiểm tra chuẩn định dạng mã nguồn Python (Flake8/Black)
→ Nếu tất cả các bước Pass -> Cho phép Reviewer bấm Merge code

```

### 11.3. Quy trình triển khai liên tục CD

```text
Khi code được hợp nhất thành công vào nhánh chính 'main'
→ GitHub Actions kích hoạt tiến trình đóng gói Docker Image
→ Đẩy các Image lên Docker Hub / GitHub Packages
→ Kết nối tự động tới máy chủ VPS thông qua SSH
→ Kéo ảnh mới: docker compose pull && docker compose up -d
→ Chạy script kiểm tra /actuator/health của Spring Boot và /health của FastAPI
→ Nếu hệ thống sống khỏe, bắn Webhook thông báo thành công về nhóm Telegram

```

---

## 12. Hướng Dẫn Thiết Lập Môi Trường Phát Triển Local

### 12.1. Công Cụ Bắt Buộc

* Hệ thống quản lý mã nguồn: **Git**
* Môi trường ảo hóa: **Docker Desktop**
* Bộ phát triển phần mềm: **Java JDK 17 hoặc 21**
* Trình quản lý gói Java: **Maven**
* Môi trường chạy NodeJS: **Node.js LTS**
* Ngôn ngữ AI: **Python 3.11+**
* Trình biên dịch khuyên dùng: **IntelliJ IDEA** (Cho Backend) và **VS Code** (Cho Frontend/AI)

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

Đảm bảo `mentor-postgres` (5432) và `mentor-redis` (6379) đang chạy.

### 12.4. Khởi Động Backend API (Java Spring Boot)

Mở toàn bộ thư mục `backend/mentor-api` bằng IntelliJ IDEA (IDE sẽ tự động nhận diện cấu trúc Maven Multi-Module).

Hoặc chạy thông qua Terminal bằng Maven:

```bash
cd backend/mentor-api
mvn clean install
mvn spring-boot:run -pl mentor-web

```

Server Spring Boot sẽ khởi chạy ở cổng mặc định (ví dụ: `8080` hoặc cấu hình riêng ở `.env`).

### 12.5. Cài Đặt AI Service

```bash
cd services/ai-service
python -m venv .venv
# Kích hoạt môi trường ảo:
.venv\Scripts\activate # (Windows) hoặc source .venv/bin/activate (Mac/Linux)
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000

```

### 12.6. Cấu Hình Các Nhánh Frontend

Khởi chạy Giao diện dành cho Học viên :

```bash
cd frontend/mentee-web
npm install
npm run dev

```

Khởi chạy Giao diện dành cho Cố vấn và Quản trị viên:

```bash
cd frontend/admin-mentor-web
npm install
npm run dev

```

---

## 13. Danh Sách Quản Lý Biến Môi Trường (`.env`)

Tạo tệp cấu hình `.env` tại thư mục gốc dựa trên mẫu `.env.example`:

```env
# Cấu hình kết nối cơ sở dữ liệu quan hệ PostgreSQL
POSTGRES_USER=mentor_admin
POSTGRES_PASSWORD=mentor_secure_pass_2026
POSTGRES_DB=mentor_hub_db
POSTGRES_PORT=5432

# Điểm neo cổng kết nối dịch vụ
SPRING_SERVER_PORT=8080
AI_SERVICE_PORT=8000

# Cấu hình bảo mật và khóa xác thực danh tính (JJWT)
JWT_SECRET=super-secret-key-for-mentor-hub-system-architecture-2026-java
JWT_EXPIRY_DAYS=7

# Khóa bảo mật kết nối dịch vụ trí tuệ nhân tạo lõi
GEMINI_API_KEY=AIzaSyYourActualGeminiKeyHere_To_Be_Changed

# Cấu hình cổng thông báo qua Telegram Bot
TELEGRAM_BOT_TOKEN=123456789:ABCdefGhIJKlmNoPQRsTUVwxyZ
TELEGRAM_CHAT_ID=-987654321

```

*Tuyệt đối nghiêm cấm việc commit tệp tin chứa mật khẩu thực tế lên GitHub.*

---

## 14. Mô Hình Quản Lý Nhánh Git Workflow

Dự án áp dụng mô hình phân nhánh chuẩn:

```text
main      -> Nhánh phân phối chính thức (Môi trường Production/Demo)
develop   -> Nhánh tích hợp trung tâm kiểm thử
feature/* -> Nhánh tính năng biệt lập theo Issue

```

Quy trình phát triển một tính năng:

```bash
git checkout develop
git pull origin develop
git checkout -b feature/issue-10-connect-websocket-stomp

# Lập trình, test local

git add .
git commit -m "feat: triển khai kết nối hoàn chỉnh cổng tín hiệu WebSocket STOMP"
git push -u origin feature/issue-10-connect-websocket-stomp

```

Tạo **Pull Request**: `feature/*` → `develop`. Khi hoàn thiện đồ án: `develop` → `main`.

---

## 15. Tiêu Chuẩn Quản Lý Task Và Kiểm Duyệt Code

### 15.1. Định Nghĩa Issue

Mỗi Issue trên GitHub phải bao gồm:

* **Mục tiêu**: Tính năng cần làm.
* **Phạm vi tác động**: Module nào trong kiến trúc Maven bị chỉnh sửa (vd: `mentor-application`, `mentor-infrastructure`).
* **API Contract**: Cấu trúc Request/Response nếu có Endpoint mới.
* **Định nghĩa hoàn thành**: Build Maven thành công, Pass Unit Test, không lộ Secret.

### 15.2. Quy trình tạo Pull Request

Mẫu mô tả PR bắt buộc:

```markdown
## Tóm tắt nội dung thay đổi
- Bổ sung cấu hình WebSocketConfig trong mentor-infrastructure
- Thêm filter chặn Token JWT trên luồng Socket ở mentor-web

## Khớp nối Issue liên quan
Closes #10

## Bảng kiểm tra điều kiện (Checklist)
- [ ] Code đã biên dịch thành công (Maven Build Pass)
- [ ] Đã chạy qua các kịch bản kiểm thử (JUnit Test Pass)
- [ ] Không vô tình commit cấu hình mật khẩu thật

```

---

## 16. Kế Hoạch Khởi Tạo Các Khối Công Việc Ban Đầu

Danh sách các Issue nền tảng cần phân chia ngay cho đội ngũ 5 thành viên:

```text
[ARCH] Thiết lập cấu trúc Multi-Module Maven, file pom.xml cha và các pom.xml con.
[DEVOPS] Khởi tạo tệp cấu hình Docker Compose thiết lập môi trường Postgres và Redis cho local.
[BE] Thiết lập hệ thống cấu trúc gói (package) và kết nối Spring Data JPA với PostgreSQL.
[BE] Xây dựng Identity Module: Cấu hình Spring Security, phân quyền và cấp phát JWT.
[BE] Cấu hình Spring WebSocket & STOMP cho kiến trúc Realtime giao tiếp nội bộ.
[FE] Khởi tạo cấu trúc dự án Mentee Web Client (Next.js/React).
[FE] Khởi tạo cấu trúc dự án Admin & Mentor Dashboard.
[AI] Khởi tạo khung mã nguồn độc lập FastAPI AI Service và cấu hình các route cơ bản.
[AI] Xây dựng cấu trúc kho dữ liệu tri thức Knowledge Base và viết hàm nhúng dữ liệu đầu tiên.
[DOCS] Hoàn thiện chi tiết đặc tả thiết kế cấu trúc bảng dữ liệu (Database Schema) bằng ERD.

```

---

## 17. Kịch Bản Nghiệm Thu & Demo Sản Phẩm

1. Triển khai toàn bộ hệ thống bằng Docker Compose để chứng minh hạ tầng sạch.
2. Trình bày trang GitHub hiển thị lịch sử Issues/Pull Requests.
3. Show kết quả tự động chạy kiểm thử thành công của luồng CI GitHub Actions (Maven Test).
4. Đăng nhập đồng thời 3 vai trò: Học viên, Cố vấn và Admin.
5. Thực hiện quy trình Mentor đăng ký tài khoản, đăng tải bảng điểm và xem AI phân tích hồ sơ tự động.
6. Admin phê duyệt Mentor, Mentor thiết lập biểu phí và bật Online.
7. Học viên tìm Mentor, thực hiện lệnh gọi trực tuyến thời gian thực.
8. Trình diễn màn hình đổ chuông, đồng ý kết nối WebRTC và Job Scheduler (Spring `@Scheduled`) trừ tiền ví điện tử tự động sau mỗi 1 phút.
9. Cúp máy, show hóa đơn giao dịch quyết toán tài chính lưu tại Database.
10. Học viên đặt câu hỏi cho Trợ lý AI để truy xuất kiến thức dựa trên dữ liệu RAG.

---

## 18. Lộ Trình Nâng Cấp Và Phát Triển Tương Lai

* Tách biệt module `wallet` và `session` thành Microservices độc lập sử dụng Spring Cloud khi quy mô hệ thống lớn.
* Tích hợp Message Broker **RabbitMQ/Kafka** xử lý các tác vụ bất đồng bộ nặng (Gửi mail biên lai, log cuộc gọi).
* Giám sát hiệu năng hệ thống chuyên sâu bằng Prometheus kết hợp Grafana, lấy metric từ Spring Boot Actuator.
* Kết nối trực tiếp môi trường Sandbox của các cổng thanh toán Việt Nam (MoMo, VNPAY).

---

## 19. Văn Hóa Và Quy Tắc Phối Hợp Trong Nhóm

* Nghiêm cấm commit trực tiếp lên `main` và `develop`.
* Bất kỳ thay đổi cấu trúc API nào phải được cập nhật vào `docs/api-contract.md`.
* Chỉnh sửa bảng Database Entity (JPA) phải cập nhật sơ đồ `docs/db-schema.md`.
* Chỉ ghi thông tin ảo vào `.env.example`.
* Mỗi Pull Request gửi đi phải kèm hình ảnh/video minh chứng tính năng đã chạy thành công.

---

## 20. Tình Trạng Hiện Tại & Phạm Vi Nghiệm Thu

Kiến trúc mục tiêu tổng thể của đồ án:

```text
Modular Monolith Java Spring Boot + FastAPI AI RAG + Realtime WebSocket STOMP + Dockerized CI/CD

```

Phạm vi tính năng bắt buộc hoàn thiện cho buổi báo cáo:

```text
- Đăng nhập, phân quyền, xác thực bằng Spring Security JWT.
- Trang hồ sơ Mentor, nút bật/tắt Online.
- Tìm kiếm, lọc danh sách Mentor trực tuyến.
- Luồng cuộc gọi WebRTC điều phối qua Spring WebSocket.
- Job Scheduler mô phỏng tính phí theo phút và quyết toán ví.
- Dashboard thống kê và kiểm duyệt cho Admin.
- Trợ lý AI RAG trả lời kiến thức nền tảng giáo trình.
- Đóng gói Docker toàn bộ hệ thống.

```
