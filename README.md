<p align="center">
  <img src="https://i.pinimg.com/originals/fd/91/b1/fd91b1715061efc79dbb6678aea0f9b9.gif" width="220" alt="Ngọc Rồng Online">
</p>

<h1 align="center">HDG Ecosystem — RIPT1307 Nhóm 01</h1>

<p align="center">
  Phạm Hải Đăng &nbsp;·&nbsp; Lê Đình Thành &nbsp;·&nbsp; Lê Xuân Dũng
</p>

---

## Điểm khác biệt của nhóm

Thay vì làm chung một sản phẩm, mỗi thành viên phát triển **một hệ thống riêng hoàn chỉnh** — khác ngôn ngữ, khác hạ tầng, khác nghiệp vụ — nhưng cùng thuộc một hệ sinh thái công ty **HDG**, chia sẻ chung phần auth, user và payment backend.

```
                     ┌─────────────────────┐
                     │    HDG Ecosystem     │
                     └──────────┬──────────┘
          ┌───────────────────── ┼ ─────────────────────┐
          ▼                      ▼                      ▼
┌──────────────────┐   ┌─────────────────┐   ┌──────────────────┐
│  Ngọc Rồng Online│   │ HDG Admin & HR  │   │ HDG Healthcare   │
│   (Hải Đăng)     │   │  (Đình Thành)   │   │   (Xuân Dũng)    │
│ 14 microservices │   │ Web · Mobile    │   │ FastAPI · React  │
└──────────────────┘   └─────────────────┘   └──────────────────┘
          │                      │                      │
          └──────────────────────┴──────────────────────┘
                   Dùng chung: auth · user · payment
```

---

## Phạm Hải Đăng — Ngọc Rồng Online Platform

> **Role:** Full Stack · Solution Architect · BA · DBA · DevSecOps · SRE · QA · Game Developer · Technical Writer  
> **Stack:** TypeScript (NestJS · Next.js) · Go · Java (LibGDX) · Docker · Nginx · Cloudflare  
> **Quy mô:** 18 repos · 14 microservices · 49 app instances · 3 VPS · production 24/7  
> **Tài liệu BA:** [docs/architecture.md](https://github.com/DANG-PH/dragonboy-api-gateway/blob/master/docs/architecture.md)  
> **Tài liệu QA:** [docs/metrics.md](https://github.com/DANG-PH/dragonboy-api-gateway/blob/master/docs/metrics.md) — stress test & soak test, breaking point ~1500 RPS, capacity analysis

Tái hiện MMORPG Ngọc Rồng Online — game client Java/LibGDX, web platform Next.js, thanh toán thực tế qua VietQR/PayOS (webhook + idempotency), chatbot RAG hỏi đáp tài liệu game (Gemini embedding + LLM), và hạ tầng phân tán tự vận hành trên 3 VPS. Kiến trúc microservices 14 service giao tiếp qua gRPC + event-driven (RabbitMQ), giao dịch liên-service đảm bảo nhất quán bằng Saga + Outbox Pattern. Bảo mật theo mô hình Defense in Depth (Cloudflare → Nginx → API Gateway → App → DB), xác thực hai lớp (mật khẩu + OTP email), JWT versioning. CI/CD tự động qua YAML với health check + auto rollback, monitoring Prometheus/Grafana, distributed tracing Jaeger, backup định kỳ lên Google Drive, alerting Discord/Telegram. Đã kiểm thử stress test và soak test thực tế.

**Production:** [ngocrongdark.com](https://ngocrongdark.com) · [api.ngocrongdark.com](https://api.ngocrongdark.com) · [download.ngocrongdark.com](https://download.ngocrongdark.com) · [data.ngocrongdark.com](https://data.ngocrongdark.com) · [redis.ngocrongdark.com](https://redis.ngocrongdark.com) · [grafana.ngocrongdark.com](https://grafana.ngocrongdark.com)

### Repositories

| Nhóm | Repo | Ngôn ngữ | Mô tả ngắn |
|---|---|---|---|
| **Client** | [dragonboy-web](https://github.com/DANG-PH/dragonboy-web) | TypeScript · Tailwind CSS | Web platform — shop, account market, leaderboard, chat, ví, AI chatbot |
| | [ngoc-rong-online](https://github.com/DANG-PH/ngoc-rong-online) | Java | Game client — multiplayer realtime, vật phẩm, nạp thẻ |
| **NestJS** | [dragonboy-api-gateway](https://github.com/DANG-PH/dragonboy-api-gateway) | TypeScript · Lua | API Gateway — routing, JWT, rate limiting, circuit breaker · kèm tài liệu BA |
| | [dragonboy-auth-service](https://github.com/DANG-PH/dragonboy-auth-service) | TypeScript | Auth — OTP 2FA, Google OAuth, JWT versioning |
| | [dragonboy-user-service](https://github.com/DANG-PH/dragonboy-user-service) | TypeScript | Player — profile, game stats, inventory, leaderboard |
| | [dragonboy-pay-service](https://github.com/DANG-PH/dragonboy-pay-service) | TypeScript | Ví — nạp QR (VietQR/PayOS), idempotency, lịch sử giao dịch |
| | [dragonboy-item-service-go](https://github.com/DANG-PH/dragonboy-item-service-go) | Golang · Lua | Inventory — vật phẩm người chơi, bulk insert, UUID lookup |
| | [dragonboy-social-network-service](https://github.com/DANG-PH/dragonboy-social-network-service) | TypeScript | Mạng xã hội — bạn bè, chat, group, comment, thông báo |
| | [dragonboy-game-service](https://github.com/DANG-PH/dragonboy-game-service) | TypeScript · Lua | Game NestJS — stateful events, phối hợp Go realtime |
| | [dragonboy-game-data-service](https://github.com/DANG-PH/dragonboy-game-data-service) | TypeScript | Master data — maps, NPCs, items, shops, nhạc nền runtime |
| | [dragonboy-queue-service](https://github.com/DANG-PH/dragonboy-queue-service) | TypeScript | Async queue — RabbitMQ, email, item sync, retry |
| | [dragonboy-disciple-service](https://github.com/DANG-PH/dragonboy-disciple-service) | TypeScript | Đệ tử — tạo, theo dõi sức mạnh, trạng thái theo player |
| | [dragonboy-admin-service](https://github.com/DANG-PH/dragonboy-admin-service) | TypeScript | Admin — RBAC, tài chính, saga mua bán tài khoản |
| **Golang** | [dragonboy-game-service-go](https://github.com/DANG-PH/dragonboy-game-service-go) | Golang · Lua | Realtime engine — WebSocket, binary protocol, NATS, 20Hz tick |
| **Infra** | [dragonboy-devops-service](https://github.com/DANG-PH/dragonboy-devops-service) | YAML | CI/CD hub — orchestrate deploy tự động 14 services lên 3 VPS |
| | [dragonboy-nginx-service](https://github.com/DANG-PH/dragonboy-nginx-service) | Shell | Load balancer, reverse proxy, SSL, Docker Compose |
| | [dragonboy-db-backups](https://github.com/DANG-PH/dragonboy-db-backups) | SQL | Backup tự động 4 AM — MySQL, PostgreSQL, MongoDB, Redis |
| | [dragonboy-deploy-scripts](https://github.com/DANG-PH/dragonboy-deploy-scripts) | Shell | Bootstrap VPS mới — Node.js, Go, PM2, UFW, swap, multi-service setup |

---

## Lê Đình Thành — HDG Admin & HR System

> **Role:** Full Stack · System Designer · BA · QA  
> **Stack:** TypeScript (Express · React Native / Expo · UmiJS) · JavaScript (Express) · MongoDB · Redis · RabbitMQ · Socket.IO · Tailwind CSS (NativeWind) · Ant Design v5 · Cloudinary  
> **Quy mô:** 9 repos · 7 microservices · 1 web client · 1 mobile app client

Hệ thống quản lý nội bộ và nhân sự tích hợp trực tiếp vào hệ sinh thái chung HDG.

Ứng dụng di động đa nền tảng (React Native/Expo) sử dụng giao diện Tailwind CSS (NativeWind) mang lại trải nghiệm mượt mà, hỗ trợ nhân viên đăng ký lịch làm việc theo tuần (Office/Remote/Nghỉ phép), quét mã QR chấm công check-in/out thời gian thực qua camera di động, quản lý danh sách công việc (Todo/Task) và nhắn tin trò chuyện nội bộ.

Hệ thống quản trị Admin cung cấp các tính năng quản lý nhân sự chuyên sâu như phê duyệt đơn đăng ký lịch làm việc (hỗ trợ duyệt hàng loạt), thống kê mật độ làm việc (Heatmap) theo ngày và tuần, cấu hình quy định chấm công/deadline và tạo mã QR chấm công động thời gian thực (giới hạn 30 giây bảo mật tối đa).

**HDG Admin (Web Client)** được phát triển dựa trên **UmiJS** và **Ant Design v5**, tích hợp các chức năng quản trị toàn diện: thống kê tài chính và biểu đồ doanh thu dòng tiền (ApexCharts), phê duyệt yêu cầu rút tiền (cashout), quản lý tin tức (hỗ trợ trình soạn thảo TinyMCE, khóa bài viết), quản lý người chơi (tra cứu profile bằng Auth ID, khóa/mở khóa tài khoản có thời hạn, gửi email hệ thống), và quản lý cấu hình game (NPC spawn, bản đồ, CRUD vật phẩm bán trong shop NPC).

Kiến trúc backend phân tán (Microservices) gồm 7 dịch vụ độc lập giao tiếp qua API Gateway (định tuyến, proxy WebSocket cho Socket.io và tự động gộp tài liệu Swagger API). Xử lý tác vụ gửi email OTP xác thực tài khoản bất đồng bộ thông qua RabbitMQ và Nodemailer SMTP. Quản lý trạng thái và mã xác thực bảo mật được lưu trữ trong bộ nhớ đệm Redis để tối ưu hóa hiệu năng.

### Repositories

| Nhóm | Repo | Ngôn ngữ | Mô tả ngắn |
|---|---|---|---|
| **Web Client** | [adminwebnr](https://github.com/lethanh2006/adminwebnr) | TypeScript · UmiJS · Ant Design | Trang quản trị Admin (HDG Admin) - Quản lý người chơi (tra cứu, khóa/mở khóa, gửi email), quản lý tin tức (TinyMCE), quản lý game (bản đồ, NPC, NPC shop), duyệt rút tiền (cashout), và thống kê doanh thu (ApexCharts). |
| **Mobile Client** | [Nrapp](https://github.com/lethanh2006/Nrapp) | TypeScript · Tailwind CSS | Ứng dụng di động Expo/React Native cho nhân viên và admin - quản lý lịch làm việc, nhiệm vụ (Todo), chat realtime, quét QR chấm công qua camera. |
| **Backend** | [API-GATEWAY](https://github.com/lethanh2006/API-GATEWAY) | JavaScript | API Gateway - điều phối định tuyến, xử lý proxy Socket.io chat, gộp và phục vụ tài liệu Swagger API tập trung. |
| | [USER_SERVICE](https://github.com/lethanh2006/USER_SERVICE) | TypeScript | Dịch vụ người dùng & xác thực - đăng ký, đăng nhập, hồ sơ cá nhân (`/me`), phân quyền, xác thực 2 lớp OTP, tích hợp cache Redis. |
| | [WORKSCHEDULE_SERVICE](https://github.com/lethanh2006/WORKSCHEDULE_SERVICE) | TypeScript | Dịch vụ lịch làm việc & chấm công - tạo mã QR check-in động (hạn 30s), ghi nhận check-in/out, quản lý và phê duyệt lịch làm việc tuần, heatmap. |
| | [CHAT_SERVICE](https://github.com/lethanh2006/CHAT_SERVICE) | TypeScript | Dịch vụ trò chuyện thời gian thực - giao tiếp qua Socket.io, lưu trữ tin nhắn văn bản và hình ảnh tải lên qua Cloudinary. |
| | [TODO_SERVICE](https://github.com/lethanh2006/TODO_SERVICE) | TypeScript | Dịch vụ quản lý công việc (Todo) - tạo nhiệm vụ, phân công, cập nhật trạng thái, độ ưu tiên và thời hạn. |
| | [MAIL_SERVICE](https://github.com/lethanh2006/MAIL_SERVICE) | TypeScript | Dịch vụ gửi email tự động - tiêu thụ hàng đợi `send-otp` từ RabbitMQ, gửi email mã xác thực qua SMTP Gmail/Nodemailer. |
| | [Logger](https://github.com/lethanh2006/Logger) | JavaScript | Dịch vụ ghi log tập trung - cung cấp API tiếp nhận log từ các microservices khác để lưu trữ file log bằng Winston (`combined.log`, `error.log`). |

---

## Lê Xuân Dũng — HDG Healthcare Management

> **Role:** Full Stack · System Designer · BA · QA  
> **Stack:** TypeScript (React · Vite) · Python (FastAPI) · PostgreSQL · Redis · Docker  
> **Quy mô:** 4 repos · 1 frontend · 1 backend · production-ready

Hệ thống quản lý sức khỏe nhân viên nội bộ cho hệ sinh thái HDG — cho phép nhân viên khai báo hồ sơ sức khỏe cá nhân, đặt lịch khám định kỳ, và theo dõi các chỉ số sức khỏe theo thời gian. Kết nối xác thực tập trung qua HDG Auth Service (JWT), đồng bộ dữ liệu nhân sự từ HDG HR Service.

Backend xây dựng trên **FastAPI** (Python) với cấu trúc module hóa theo domain, tích hợp **PostgreSQL** lưu trữ hồ sơ và lịch sử khám, **Redis** cache session và OTP token, tài liệu API tự động qua Swagger/OpenAPI. Frontend **React + Vite + Tailwind CSS** kết nối SSO qua HDG Ecosystem, dashboard tổng quan sức khỏe cá nhân với biểu đồ theo dõi chỉ số. Phân quyền hai vai trò: **nhân viên** (xem và cập nhật hồ sơ, đặt lịch, theo dõi cá nhân) và **admin/y tế** (quản lý lịch khám toàn công ty, phê duyệt, thống kê tổng hợp).

### Repositories

| Nhóm | Repo | Ngôn ngữ | Mô tả ngắn |
|---|---|---|---|
| **Frontend** | [Healthcare-Frontend](https://github.com/DungLe0102/Healtcare-Frontend) | TypeScript · React · Vite · Tailwind CSS | Web client — dashboard sức khỏe cá nhân, đặt lịch khám, lịch sử khám bệnh, khai báo & cập nhật hồ sơ sức khỏe, biểu đồ theo dõi chỉ số |
| **Backend** | [Healthcare-Backend](https://github.com/DungLe0102/FASTAPI-HEALTHCARE) | Python · FastAPI · PostgreSQL · Redis | REST API — quản lý hồ sơ sức khỏe, lịch khám, theo dõi chỉ số (BMI, huyết áp, đường huyết…), tích hợp HDG Auth, Swagger docs |

---

<p align="center"><sub>HDG Ecosystem · RIPT1307 Nhóm 01 · 2025–2026</sub></p>
