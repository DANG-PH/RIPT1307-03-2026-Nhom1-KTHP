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
          │                      │
          └──────────────────────┘
             Dùng chung: auth · user · payment
```

---

## Phạm Hải Đăng — Ngọc Rồng Online Platform

> **Stack:** NestJS · Next.js · Golang · Java (LibGDX) · Docker · Nginx · Cloudflare  
> **Quy mô:** 14 microservices · 47 instances · 3 VPS · production 24/7  
> **Tài liệu BA:** [docs/architecture.md](https://github.com/DANG-PH/dragonboy-api-gateway/blob/master/docs/architecture.md)

Tái hiện game MMORPG Ngọc Rồng Online — game client Java, web platform Next.js, thanh toán VietQR/PayOS, chatbot RAG (Gemini), hạ tầng phân tán 3 VPS. Bảo mật theo mô hình Defense in Depth, có stress test và soak test.

**Production:** [ngocrongdark.com](https://ngocrongdark.com) · [api.ngocrongdark.com](https://api.ngocrongdark.com) · [download.ngocrongdark.com](https://download.ngocrongdark.com) · [data.ngocrongdark.com](https://data.ngocrongdark.com) · [redis.ngocrongdark.com](https://redis.ngocrongdark.com) · [grafana.ngocrongdark.com](https://grafana.ngocrongdark.com)

### Repositories

| Nhóm | Repo | Mô tả ngắn |
|---|---|---|
| **Client** | [dragonboy-web](https://github.com/DANG-PH/dragonboy-web) | Web Next.js — shop, account market, leaderboard, chat, ví, AI chatbot |
| | [ngoc-rong-online](https://github.com/DANG-PH/ngoc-rong-online) | Game client LibGDX/Java — multiplayer, vật phẩm, nạp thẻ |
| **NestJS** | [dragonboy-api-gateway](https://github.com/DANG-PH/dragonboy-api-gateway) | API Gateway — routing, JWT, rate limiting, circuit breaker, tài liệu BA đầy đủ |
| | [dragonboy-auth-service](https://github.com/DANG-PH/dragonboy-auth-service) | Auth — OTP 2FA, Google OAuth, JWT versioning |
| | [dragonboy-user-service](https://github.com/DANG-PH/dragonboy-user-service) | Player — profile, game stats, inventory, leaderboard |
| | [dragonboy-pay-service](https://github.com/DANG-PH/dragonboy-pay-service) | Ví — nạp QR (VietQR/PayOS), idempotency, lịch sử giao dịch |
| | [dragonboy-item-service](https://github.com/DANG-PH/dragonboy-item-service) | Inventory — CRUD vật phẩm, bulk insert, UUID lookup |
| | [dragonboy-social-network-service](https://github.com/DANG-PH/dragonboy-social-network-service) | Mạng xã hội — bạn bè, chat, group, comment, thông báo |
| | [dragonboy-game-service](https://github.com/DANG-PH/dragonboy-game-service) | Game NestJS — stateful events, phối hợp Go realtime |
| | [dragonboy-game-data-service](https://github.com/DANG-PH/dragonboy-game-data-service) | Master data — maps, NPCs, items, shops, nhạc nền runtime |
| | [dragonboy-queue-service](https://github.com/DANG-PH/dragonboy-queue-service) | Async queue — RabbitMQ, email, item sync, retry |
| | [dragonboy-disciple-service](https://github.com/DANG-PH/dragonboy-disciple-service) | Đệ tử — tạo, theo dõi sức mạnh, trạng thái theo player |
| | [dragonboy-admin-service](https://github.com/DANG-PH/dragonboy-admin-service) | Admin — RBAC, tài chính, saga mua bán tài khoản |
| **Golang** | [dragonboy-game-service-go](https://github.com/DANG-PH/dragonboy-game-service-go) | Realtime engine — WebSocket, binary protocol, NATS, 20Hz tick |
| **Infra** | [dragonboy-devops-service](https://github.com/DANG-PH/dragonboy-devops-service) | CI/CD hub — tự động deploy 14 services lên 3 VPS |
| | [dragonboy-nginx-service](https://github.com/DANG-PH/dragonboy-nginx-service) | Nginx — load balancer, reverse proxy, SSL, Docker Compose |
| | [dragonboy-db-backups](https://github.com/DANG-PH/dragonboy-db-backups) | Backup tự động 4 AM — MySQL, PostgreSQL, MongoDB, Redis, versioned history |
| | [dragonboy-deploy-scripts](https://github.com/DANG-PH/dragonboy-deploy-scripts) | Bootstrap scripts — khởi tạo VPS mới, cài Node.js/Go/PM2/UFW/swap |

---

## Lê Đình Thành — HDG Admin & HR System

> **Stack:** Next.js · React Native · Express.js

Hệ thống quản trị nội bộ và nhân sự — web admin, app Android cho nhân viên, đặt lịch ca làm. Tích hợp trực tiếp backend auth/user/payment của Hải Đăng vào hệ sinh thái chung.

| Repo | Mô tả |
|---|---|
| *(Đình Thành bổ sung)* | |

---

## Lê Xuân Dũng — HDG Healthcare Management

> **Stack:** React · Python (FastAPI)

Hệ thống quản lý sức khỏe nhân viên — hồ sơ sức khỏe, lịch khám, theo dõi tình trạng. Hạ tầng độc lập, kết nối hệ sinh thái HDG qua auth và dữ liệu nhân sự chung.

| Repo | Mô tả |
|---|---|
| *(Xuân Dũng bổ sung)* | |

---

<p align="center"><sub>HDG Ecosystem · RIPT1307 Nhóm 01 · 2025–2026</sub></p>
