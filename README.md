<p align="center">
  <img src="https://scontent.fhan5-8.fna.fbcdn.net/v/t39.30808-6/722408523_1012012048242429_5382682113467205752_n.jpg?stp=dst-jpg_tt6&cstp=mx350x350&ctp=s350x350&_nc_cat=108&ccb=1-7&_nc_sid=a5f93a&_nc_eui2=AeEm4z1AYdtChrmkL0eb-dOwKs93keUfCoYqz3eR5R8KhsoxqXxOkNpwEIC6YUiKx3na4A26_IPBu17h-vnIyDKk&_nc_ohc=of258jfTkbMQ7kNvwHasYtf&_nc_oc=Adq9VLqe95fMVW-Bg62X1CBTnLnytsDzY12TXLXPybVrdDgj5cAVpmJPpY9xjsZRe48&_nc_zt=23&_nc_ht=scontent.fhan5-8.fna&_nc_gid=tp_RUD7xUebuV3JFUFkfDA&_nc_ss=7b2a8&oh=00_Af8J3OuJ1HOuIx6tmcIV7wbi7I-ZzzPn1bwkgU5LjPHGSA&oe=6A2FF314" width="220" alt="Ngọc Rồng Online">
</p>

<h1 align="center">HDG Ecosystem — RIPT1307 Nhóm 01, Lớp 3</h1>

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

> **Role:** Full Stack · Solution Architect · BA · DBA · DevSecOps · SRE · QA · Game Developer · Technical Writer<br>
> **Stack:** TypeScript (NestJS · Next.js) · Golang · Java (LibGDX) · Docker · Nginx · Cloudflare · AWS S3<br>
> **Quy mô:** 18 repos · 14 microservices · 1000+ commits · 49 app instances · 3 VPS · production 24/7<br>
> **Tài liệu BA:** [docs/architecture.md](https://github.com/DANG-PH/dragonboy-api-gateway/blob/master/docs/architecture.md)<br>
> **Tài liệu QA:** [docs/metrics.md](https://github.com/DANG-PH/dragonboy-api-gateway/blob/master/docs/metrics.md) — stress test & soak test, breaking point ~1500 RPS, capacity analysis

**Sản phẩm.** Một **Game MMORPG 2D nhiều người chơi trực tuyến** (tái hiện game Ngọc Rồng Online — MMORPG Dragon Ball của Việt Nam) — **solo-build hoàn chỉnh từ game client tới hạ tầng phân tán, chạy production thật 24/7 hơn 14 tháng với người dùng và doanh thu thực, cộng đồng ~10k followers trên Facebook**. Gồm game client Java/LibGDX (multiplayer realtime, kho đồ, chỉ số nhân vật), web cổng người chơi Next.js (shop, leaderboard, sàn mua bán tài khoản, chatbot AI), thanh toán thực qua VietQR/PayOS có webhook idempotency, và backend **14 microservices polyglot** (NestJS + Go) tự vận hành trên 3 VPS Ubuntu cluster.

**Kiến trúc.** Microservices giao tiếp qua gRPC + event-driven (RabbitMQ / NATS / BullMQ), **100+ endpoint trên 8 database** (PostgreSQL/MySQL transactional, MongoDB logging, Redis cache/lock); giao dịch liên-service nhất quán bằng **Saga + Outbox + Compensation** — *0% partial-failure* trên các luồng tiền và mua bán tài khoản; webhook thanh toán **VietQR/PayOS đạt 100% accuracy** qua ~100 test case integration. Bảo mật **Defense in Depth** (Cloudflare → Nginx → Gateway → App → DB), 2FA mật khẩu + OTP email, JWT versioning. CI/CD dispatch trung tâm với auto rollback (**520+ deploys, ~95% success**), observability Prometheus / Grafana / Jaeger phát hiện và xử lý **25 production incidents**, backup hằng ngày 4 AM lên Google Drive và Github Repo.

**Engineering highlights.** Migrate realtime engine từ NestJS/Socket.IO sang **Go raw WebSocket + Protobuf + NATS** giảm **~60% payload**, đạt tickrate 20Hz ổn định. **Dirty Flag + async batch writes** giảm **~90% DB write**, **Fire-and-Forget** tiết kiệm ~10ms latency, chatbot **RAG (Gemini)** với cache đạt ~40% hit rate, **–50% chi phí LLM**. Đo hiệu năng thực bằng k6: **soak 1000 RPS, p99 = 234ms, 98.4% success**; stress test breaking point ~1500 RPS; capacity production-safe **700 RPS với 30% headroom**.

### Repositories

| Nhóm | Repo | Ngôn ngữ | Mô tả ngắn |
|---|---|---|---|
| **NextJS & LibGDX (Client)** | [dragonboy-web](https://github.com/DANG-PH/dragonboy-web) | TypeScript · Tailwind CSS | Web platform — shop, account market, leaderboard, chat, ví, AI chatbot |
| | [ngoc-rong-online](https://github.com/DANG-PH/ngoc-rong-online) | Java · LibGDX | Game client — multiplayer realtime, vật phẩm, nạp thẻ |
| **Golang (Server)** | [dragonboy-game-service-go](https://github.com/DANG-PH/dragonboy-game-service-go) | Golang · Lua | Realtime engine — WebSocket, binary protocol, NATS, 20Hz tick |
| | [dragonboy-item-service-go](https://github.com/DANG-PH/dragonboy-item-service-go) | Golang | Inventory — vật phẩm người chơi, bulk insert, UUID lookup |
| **NestJS (Server)** | [dragonboy-api-gateway](https://github.com/DANG-PH/dragonboy-api-gateway) | TypeScript · Lua | API Gateway — routing, JWT, rate limiting, circuit breaker · kèm tài liệu BA |
| | [dragonboy-auth-service](https://github.com/DANG-PH/dragonboy-auth-service) | TypeScript | Auth — OTP 2FA, Google OAuth, JWT versioning |
| | [dragonboy-user-service](https://github.com/DANG-PH/dragonboy-user-service) | TypeScript | Player — profile, game stats, inventory, leaderboard |
| | [dragonboy-pay-service](https://github.com/DANG-PH/dragonboy-pay-service) | TypeScript | Ví — nạp QR (VietQR/PayOS), idempotency, lịch sử giao dịch |
| | [dragonboy-social-network-service](https://github.com/DANG-PH/dragonboy-social-network-service) | TypeScript | Mạng xã hội — bạn bè, chat, group, comment, thông báo |
| | [dragonboy-game-service](https://github.com/DANG-PH/dragonboy-game-service) | TypeScript · Lua | Game NestJS — stateful events, phối hợp Go realtime |
| | [dragonboy-game-data-service](https://github.com/DANG-PH/dragonboy-game-data-service) | TypeScript | Master data — maps, NPCs, items, shops, nhạc nền runtime |
| | [dragonboy-queue-service](https://github.com/DANG-PH/dragonboy-queue-service) | TypeScript | Async queue — RabbitMQ, email, item sync, retry |
| | [dragonboy-disciple-service](https://github.com/DANG-PH/dragonboy-disciple-service) | TypeScript | Đệ tử — tạo, theo dõi sức mạnh, trạng thái theo player |
| | [dragonboy-admin-service](https://github.com/DANG-PH/dragonboy-admin-service) | TypeScript | Admin — RBAC, tài chính, saga mua bán tài khoản |
| **Infra** | [dragonboy-devops-service](https://github.com/DANG-PH/dragonboy-devops-service) | YAML | CI/CD hub — orchestrate deploy tự động 14 services lên 3 VPS |
| | [dragonboy-nginx-service](https://github.com/DANG-PH/dragonboy-nginx-service) | Shell | Load balancer, reverse proxy, SSL, Docker Compose |
| | [dragonboy-db-backups](https://github.com/DANG-PH/dragonboy-db-backups) | SQL | Backup tự động 4 AM — MySQL, PostgreSQL, MongoDB, Redis |
| | [dragonboy-deploy-scripts](https://github.com/DANG-PH/dragonboy-deploy-scripts) | Shell | Bootstrap VPS mới — Node.js, Go, PM2, UFW, swap, multi-service setup |


**Production deployment**

- **Web & API:** [ngocrongdark.com](https://ngocrongdark.com) · [api.ngocrongdark.com](https://api.ngocrongdark.com) · [pay.ngocrongdark.com](https://pay.ngocrongdark.com) · [download.ngocrongdark.com](https://download.ngocrongdark.com)
- **Realtime WebSocket:** [ws.dangpham.id.vn](https://ws.dangpham.id.vn) · [ws-go.dangpham.id.vn](https://ws-go.dangpham.id.vn) — DNS trực tiếp, bypass Cloudflare để tối ưu latency game realtime 20Hz
- **Observability & Admin tools** (HTTP Basic Auth): [grafana.ngocrongdark.com](https://grafana.ngocrongdark.com) · [data.ngocrongdark.com](https://data.ngocrongdark.com) · [postgres.ngocrongdark.com](https://postgres.ngocrongdark.com) · [redis.ngocrongdark.com](https://redis.ngocrongdark.com)
- **Community:** [Fanpage Facebook ~10k followers](https://www.facebook.com/profile.php?id=61576541835732) — cộng đồng người chơi thật

---

## Lê Đình Thành — HDG Admin & HR System

> **Role:** Full Stack · BA · Solution Architect<br>
> **Stack:** TypeScript (Express · React Native / Expo · UmiJS) · JavaScript (Express) · MongoDB · Redis · RabbitMQ · Socket.IO · Tailwind CSS (NativeWind) · Ant Design v5 · Cloudinary<br>
> **Quy mô:** 9 repos · 7 microservices · 1 web client · 1 mobile app client

Hệ thống quản lý nội bộ và nhân sự tích hợp trực tiếp vào hệ sinh thái chung HDG.

Ứng dụng di động đa nền tảng (React Native/Expo) sử dụng giao diện Tailwind CSS (NativeWind) mang lại trải nghiệm mượt mà, hỗ trợ nhân viên đăng ký lịch làm việc theo tuần (Office/Remote/Nghỉ phép), quét mã QR chấm công check-in/out thời gian thực qua camera di động, quản lý danh sách công việc (Todo/Task) và nhắn tin trò chuyện nội bộ.

Hệ thống quản trị Admin cung cấp các tính năng quản lý nhân sự chuyên sâu như phê duyệt đơn đăng ký lịch làm việc (hỗ trợ duyệt hàng loạt), thống kê mật độ làm việc (Heatmap) theo ngày và tuần, cấu hình quy định chấm công/deadline và tạo mã QR chấm công động thời gian thực (giới hạn 30 giây bảo mật tối đa).

**HDG Admin (Web Client)** được phát triển dựa trên **UmiJS** và **Ant Design v5**, tích hợp các chức năng quản trị toàn diện: thống kê tài chính và biểu đồ doanh thu dòng tiền (ApexCharts), phê duyệt yêu cầu rút tiền (cashout), quản lý tin tức (hỗ trợ trình soạn thảo TinyMCE, khóa bài viết), quản lý người chơi (tra cứu profile bằng Auth ID, khóa/mở khóa tài khoản có thời hạn, gửi email hệ thống), và quản lý cấu hình game (NPC spawn, bản đồ, CRUD vật phẩm bán trong shop NPC).

Kiến trúc backend phân tán (Microservices) gồm 7 dịch vụ độc lập giao tiếp qua API Gateway (định tuyến, proxy WebSocket cho Socket.io và tự động gộp tài liệu Swagger API). Xử lý tác vụ gửi email OTP xác thực tài khoản bất đồng bộ thông qua RabbitMQ và Nodemailer SMTP. Quản lý trạng thái và mã xác thực bảo mật được lưu trữ trong bộ nhớ đệm Redis để tối ưu hóa hiệu năng.

### Repositories

| Nhóm | Repo | Ngôn ngữ | Mô tả ngắn |
|---|---|---|---|
| **Web Client (UmiJS)** | [dragonboy-web-admin](https://github.com/lethanh2006/adminwebnr) | TypeScript | Trang quản trị Admin (HDG Admin) - Quản lý người chơi (tra cứu, khóa/mở khóa, gửi email), quản lý tin tức (TinyMCE), quản lý game (bản đồ, NPC, NPC shop), duyệt rút tiền (cashout), và thống kê doanh thu (ApexCharts). |
| **Mobile Client (React Native)** | [app-client](https://github.com/lethanh2006/Nrapp) | TypeScript · Tailwind CSS | Ứng dụng di động Expo/React Native cho nhân viên và admin - quản lý lịch làm việc, nhiệm vụ (Todo), chat realtime, quét QR chấm công qua camera. |
| **ExpressJS (Server)** | [app-api-gateway](https://github.com/lethanh2006/API-GATEWAY) | JavaScript | API Gateway - điều phối định tuyến, xử lý proxy Socket.io chat, gộp và phục vụ tài liệu Swagger API tập trung. |
| | [app-user-service](https://github.com/lethanh2006/USER_SERVICE) | TypeScript | Dịch vụ người dùng & xác thực - đăng ký, đăng nhập, hồ sơ cá nhân (`/me`), phân quyền, xác thực 2 lớp OTP, tích hợp cache Redis. |
| | [app-workschedule-service](https://github.com/lethanh2006/WORKSCHEDULE_SERVICE) | TypeScript | Dịch vụ lịch làm việc & chấm công - tạo mã QR check-in động (hạn 30s), ghi nhận check-in/out, quản lý và phê duyệt lịch làm việc tuần, heatmap. |
| | [app-chat-service](https://github.com/lethanh2006/CHAT_SERVICE) | TypeScript | Dịch vụ trò chuyện thời gian thực - giao tiếp qua Socket.io, lưu trữ tin nhắn văn bản và hình ảnh tải lên qua Cloudinary. |
| | [app-todo-service](https://github.com/lethanh2006/TODO_SERVICE) | TypeScript | Dịch vụ quản lý công việc (Todo) - tạo nhiệm vụ, phân công, cập nhật trạng thái, độ ưu tiên và thời hạn. |
| | [app-mail-service](https://github.com/lethanh2006/MAIL_SERVICE) | TypeScript | Dịch vụ gửi email tự động - tiêu thụ hàng đợi `send-otp` từ RabbitMQ, gửi email mã xác thực qua SMTP Gmail/Nodemailer. |
| | [app-logger-service](https://github.com/lethanh2006/Logger) | JavaScript | Dịch vụ ghi log tập trung - cung cấp API tiếp nhận log từ các microservices khác để lưu trữ file log bằng Winston (`combined.log`, `error.log`). |

---

## Lê Xuân Dũng — HDG Healthcare Management

> **Role:** Full Stack · BA · Solution Architect<br>
> **Stack:** TypeScript (React · Vite) · Python (FastAPI) · PostgreSQL · Redis · ARQ · Docker · Ngrok<br>
> **Quy mô:** 2 repos · 1 frontend · 1 backend 

Hệ thống quản lý sức khỏe và phòng khám doanh nghiệp nội bộ HDG — hồ sơ sức khỏe nhân viên, đặt lịch khám với bác sĩ, hồ sơ bệnh án, kê đơn, kho dược phẩm và thẻ Bảo hiểm Y tế (BHYT). Đồng bộ danh sách nhân sự với hệ sinh thái HDG qua export/import user.

Backend **FastAPI** (Python) kiến trúc 3 lớp Router / Service / Repository, **PostgreSQL** (SQLAlchemy + Alembic), **Redis** rate-limit + **ARQ** worker hàng đợi tác vụ nền, thanh toán **VietQR + webhook HDBank** idempotent (SELECT FOR UPDATE + Regex match chống cộng tiền hai lần khi cổng retry), hoàn tiền tự động qua VietQR refund. Điểm kỹ thuật nổi bật: **Pessimistic Lock** (`with_for_update`) chống Race Condition khi nhiều bệnh nhân tranh slot khám; **FIFO inventory** xuất thuốc theo hạn dùng kèm Batch Traceability cho rollback chính xác; **Digital Signature SHA-256** ký số hồ sơ bệnh án chống chối bỏ (Non-repudiation); tính giảm trừ **BHYT 80/20** ngay từ tầng billing với Price Snapshot bảo toàn lịch sử kế toán. Frontend **React + Vite + Tailwind** SSO HDG, phân quyền 2 vai trò bệnh nhân / admin y tế, dashboard biểu đồ theo dõi chỉ số (BMI, huyết áp, đường huyết).

### Repositories

| Nhóm | Repo | Ngôn ngữ | Mô tả ngắn |
|---|---|---|---|
| **React (Client)** | [health-client](https://github.com/DungLe0102/Healtcare-Frontend) | TypeScript · Tailwind CSS | Web client — dashboard sức khỏe cá nhân, đặt lịch khám, lịch sử khám bệnh, khai báo & cập nhật hồ sơ sức khỏe, biểu đồ theo dõi chỉ số |
| **FastAPI (Server)** | [health-server](https://github.com/DungLe0102/FASTAPI-HEALTHCARE) | Python | REST API — quản lý hồ sơ sức khỏe, lịch khám, ký số bệnh án SHA-256, FIFO inventory, BHYT 80/20, VietQR webhook idempotent, tích hợp HDG Auth, Swagger docs |

---

<p align="center"><sub>HDG Ecosystem · RIPT1307 Nhóm 01 · 2025–2026</sub></p>
