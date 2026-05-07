<p align="center">
  <img src="hdg.png" width="220" alt="HDG Logo">
</p>

<h1 align="center">HDG Ecosystem — RIPT1307 Nhóm 01</h1>

<p align="center">
  <strong>Bài tập lớn thực hành lập trình web</strong><br/>
  Phạm Hải Đăng &nbsp;·&nbsp; Lê Đình Thành &nbsp;·&nbsp; Lê Xuân Dũng
</p>

---

## Mục lục

- [Bối cảnh dự án](#bối-cảnh-dự-án)
- [Tổng quan nhóm](#tổng-quan-nhóm)
- [Phạm Hải Đăng — Ngọc Rồng Online Platform](#phạm-hải-đăng--ngọc-rồng-online-platform)
- [Lê Đình Thành — HDG Admin & HR System](#lê-đình-thành--hdg-admin--hr-system)
- [Lê Xuân Dũng — HDG Healthcare Management](#lê-xuân-dũng--hdg-healthcare-management)

---

## Bối cảnh dự án

Thay vì làm chung một sản phẩm, **Nhóm 01** chọn hướng tiếp cận khác biệt: mỗi thành viên phát triển một dự án riêng — ngôn ngữ khác nhau, hạ tầng khác nhau, nghiệp vụ khác nhau — nhưng tất cả cùng thuộc **hệ sinh thái HDG**: một công ty với nền tảng game, hệ thống quản trị nhân sự và hệ thống y tế nội bộ. Các dự án chia sẻ backend ở những điểm chung, thể hiện cả khả năng độc lập lẫn tư duy tích hợp hệ thống.

---

## Tổng quan nhóm

| | Phạm Hải Đăng | Lê Đình Thành | Lê Xuân Dũng |
|---|---|---|---|
| **Dự án** | Ngọc Rồng Online Platform | HDG Admin & HR System | HDG Healthcare Management |
| **Ngôn ngữ** | TypeScript (NestJS/Next.js) · Go · Java (LibGDX) | TypeScript (Next.js/React Native) · JavaScript (Express.js) | TypeScript (React) · Python (FastAPI) |
| **Hạ tầng** | Multi-VPS · Docker · Nginx · Cloudflare | Tích hợp backend HDG + tự dev service HR | Độc lập, giao diện riêng |
| **Role** | Full Stack · BA · DevSecOps · QA · SRE · Solution Architect | Full Stack · BA · Mobile Dev | Full Stack · BA · QA |

```
                     ┌──────────────────────────┐
                     │       HDG Ecosystem       │
                     └────────────┬─────────────┘
          ┌───────────────────────┼───────────────────────┐
          ▼                       ▼                       ▼
┌───────────────────┐   ┌─────────────────┐   ┌────────────────────┐
│  Ngọc Rồng Online │   │ HDG Admin & HR  │   │ HDG Healthcare Mgmt│
│   (Hải Đăng)      │   │  (Đình Thành)   │   │   (Xuân Dũng)      │
│  14 Microservices │   │ Web · App · HR  │   │ FastAPI · React UI │
└───────────────────┘   └─────────────────┘   └────────────────────┘
          │                       │
          └───────────────────────┘
          Dùng chung: auth, user, payment backend
```

---

## Phạm Hải Đăng — Ngọc Rồng Online Platform

> **Role:** Full Stack · BA · DevSecOps · QA · SRE · Solution Architect  
> **Stack:** TypeScript (NestJS/Next.js) · Golang · Java (LibGDX) · Docker · Nginx · Cloudflare  
> **Quy mô:** 14 microservices · 47 instances · 3 VPS · chạy 24/7 production

Tái hiện game MMORPG Ngọc Rồng Online — gồm game client, web platform người dùng, hệ thống thanh toán, chatbot AI, và toàn bộ hạ tầng phân tán. Bảo mật theo mô hình **Defense in Depth** (Cloudflare → Nginx → API Gateway → Application → Database). Kiểm thử với stress test, soak test server và unit test client.

**Production:**

| | |
|---|---|
| 🎮 Game & Web | [ngocrongdark.com](https://ngocrongdark.com) |
| 🔌 API Gateway | [api.ngocrongdark.com](https://api.ngocrongdark.com) |
| 📦 Game Releases | [download.ngocrongdark.com](https://download.ngocrongdark.com) |
| 🗄️ Database Hub | [data.ngocrongdark.com](https://data.ngocrongdark.com) |
| 📊 Redis Monitor | [redis.ngocrongdark.com](https://redis.ngocrongdark.com) |

### Repositories

**Client**

| Repo | Mô tả |
|---|---|
| [dragonboy-web](https://github.com/DANG-PH/dragonboy-web) | Web platform Next.js cho người chơi — item shop, account market, leaderboard, real-time chat, ví PayOS, và RAG chatbot AI. |
| [ngoc-rong-online](https://github.com/DANG-PH/ngoc-rong-online) | Game MMORPG LibGDX/Java — multiplayer real-time, giao dịch vật phẩm, nạp thẻ, tái hiện Ngọc Rồng gốc. |

**Server — NestJS (11 services)**

| Repo | Mô tả |
|---|---|
| [dragonboy-api-gateway](https://github.com/DANG-PH/dragonboy-api-gateway) | Cổng vào duy nhất của hệ thống — routing, auth middleware, rate limiting, distributed tracing, observability và bảo mật tầng application. |
| [dragonboy-auth-service](https://github.com/DANG-PH/dragonboy-auth-service) | Xác thực người dùng — OTP 2FA, Google OAuth, JWT refresh + token versioning; phát Redis pub/sub event khi token bị revoke để các service đồng bộ realtime. |
| [dragonboy-user-service](https://github.com/DANG-PH/dragonboy-user-service) | Quản lý player — profile, game state, in-game economy (gold & gems), inventory, leaderboard; cache hot data trên Redis. |
| [dragonboy-game-service](https://github.com/DANG-PH/dragonboy-game-service) | Business logic game phức tạp và stateful game events; nhận event từ Go service qua NATS, xử lý nghiệp vụ rồi persist xuống DB. |
| [dragonboy-game-data-service](https://github.com/DANG-PH/dragonboy-game-data-service) | Master data tĩnh của game — maps, NPCs, item definitions, NPC shops; cache toàn bộ trên Redis, source of truth cho các service khác. |
| [dragonboy-item-service](https://github.com/DANG-PH/dragonboy-item-service) | Quản lý inventory — CRUD vật phẩm, bulk insert, UUID lookup, item swap với optimistic locking và database indexing tối ưu. |
| [dragonboy-pay-service](https://github.com/DANG-PH/dragonboy-pay-service) | Ví người chơi — nạp tiền QR (PayOS), idempotency-safe balance update, lịch sử giao dịch, phát event thanh toán lên RabbitMQ để xử lý async. |
| [dragonboy-social-network-service](https://github.com/DANG-PH/dragonboy-social-network-service) | Mạng xã hội trong game — bạn bè, private chat, group room, threaded comment + like; push thông báo realtime qua Redis pub/sub. |
| [dragonboy-queue-service](https://github.com/DANG-PH/dragonboy-queue-service) | Consumer xử lý async qua RabbitMQ — gửi email (single & bulk), item sync/swap, dead-letter queue và retry logic, hỗ trợ horizontal scaling. |
| [dragonboy-disciple-service](https://github.com/DANG-PH/dragonboy-disciple-service) | Hệ thống đệ tử — tạo đệ tử, power tracking, persist trạng thái game theo từng player; expose nội bộ qua Protocol Buffers. |
| [dragonboy-admin-service](https://github.com/DANG-PH/dragonboy-admin-service) | Vận hành nội bộ — phân quyền RBAC (editor / cashier / marketplace), quản lý tài chính, partner workflows, audit log. |

**Server — Golang (1 service)**

| Repo | Mô tả |
|---|---|
| [dragonboy-game-service-go](https://github.com/DANG-PH/dragonboy-game-service-go) | Real-time game server hiệu năng cao — raw WebSocket, custom binary protocol, NATS pub/sub, tick processing độ trễ thấp. |

**Infra / DevOps (2 services)**

| Repo | Mô tả |
|---|---|
| [dragonboy-devops-service](https://github.com/DANG-PH/dragonboy-devops-service) | CI/CD hub trung tâm — nhận trigger từ 14 services, orchestrate deploy tự động lên 3 VPS riêng biệt. |
| [dragonboy-nginx-service](https://github.com/DANG-PH/dragonboy-nginx-service) | Nginx stack — load balancer, reverse proxy, SSL termination, Docker Compose trên dedicated VPS. |

---

## Lê Đình Thành — HDG Admin & HR System

> **Role:** Full Stack · BA · Mobile Dev  
> **Stack:** TypeScript (Next.js / React Native) · JavaScript (Express.js)

Xây dựng hệ thống **quản trị nội bộ và quản lý nhân sự** cho HDG — gồm web admin, app Android cho nhân viên, web đặt lịch ca làm và tự phát triển thêm service backend riêng phục vụ nghiệp vụ HR. Tận dụng và tích hợp trực tiếp backend của Hải Đăng (auth, user, payment) vào hệ sinh thái chung.

### Repositories

| Repo | Mô tả |
|---|---|
| *(Đình Thành bổ sung)* | |

---

## Lê Xuân Dũng — HDG Healthcare Management

> **Role:** Full Stack · BA · QA  
> **Stack:** TypeScript (React) · Python (FastAPI)

Xây dựng hệ thống **quản lý sức khỏe nhân viên** cho HDG — backend FastAPI, giao diện React, quản lý hồ sơ sức khỏe, lịch khám và theo dõi tình trạng nhân viên. Hạ tầng độc lập, kết nối hệ sinh thái HDG qua auth và dữ liệu nhân sự chung.

### Repositories

| Repo | Mô tả |
|---|---|
| *(Xuân Dũng bổ sung)* | |

---

<p align="center">
  <sub>HDG Ecosystem · RIPT1307 Nhóm 01 · 2025–2026</sub>
</p>
