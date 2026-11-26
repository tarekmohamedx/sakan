# Sakan - Student Housing Platform

A full-stack platform that helps students find housing: browse listings, rooms and beds, book a stay, pay online, and chat with hosts in real time. Built as a team graduation project.

**Monorepo:** `frontend/` (Angular) + `backend/` (ASP.NET Core). Both project histories were merged into this repository with full commit history preserved.

## Screenshots

> Coming soon - UI captures will live in `docs/screenshots/`.
>
> - [ ] Home / listing search
> - [ ] Listing details (rooms, beds, amenities, map)
> - [ ] Booking flow + payment
> - [ ] Real-time chat
> - [ ] Host dashboard

## Architecture

```
Angular 18 SPA (frontend/)
        |  REST API + SignalR hubs (chat, notifications)
        v
ASP.NET Core 9 API (backend/)
  Sakan/                API layer: controllers, SignalR hubs, auth
  Sakan.Application/    services, DTOs, interfaces
  Sakan.Domain/         entities and domain models
  Sakan.Infrastructure/ EF Core (SQL Server), external integrations
  Sakan.InfrastructureTests/  MSTest tests
```

## Features

- Listings with rooms, beds, amenities, photo galleries and map locations
- Booking requests with a dual-approval flow (guest and host), including real-time status notifications
- Online payments with Stripe (PaymentIntents + webhook confirmation)
- Real-time chat between guests and hosts over SignalR
- Favorites, reviews and ratings
- Host dashboard (listings, bookings, reviews) and admin panel (user management, approvals)
- Support tickets and complaints
- Google external login plus JWT authentication with ASP.NET Core Identity
- Email notifications (SendGrid / SMTP)
- Image hosting via ImageKit
- AI assistant endpoint
- Arabic/English UI (ngx-translate)

## Tech stack

| Layer    | Technologies |
|----------|--------------|
| Frontend | Angular 18 (SSR), TypeScript, Tailwind CSS, Angular Material, Leaflet maps, SignalR client, Stripe.js, Chart.js |
| Backend  | ASP.NET Core 9, EF Core 9 (SQL Server), SignalR, JWT Bearer, ASP.NET Core Identity |
| Services | Stripe, Google OAuth, ImageKit, SendGrid / MailKit |
| Testing  | MSTest |

## Getting started

### Prerequisites

- .NET 9 SDK
- Node.js 18+ and npm
- SQL Server instance

### Backend

```bash
cd backend
dotnet restore
```

Configuration lives in `backend/Sakan/appsettings.json` (a committed template with placeholder values). Put real values in [user-secrets](https://learn.microsoft.com/aspnet/core/security/app-secrets) or environment variables - never commit them:

```bash
cd backend/Sakan
dotnet user-secrets init
dotnet user-secrets set "ConnectionStrings:connection" "<your-sql-server-connection-string>"
dotnet user-secrets set "jwt:key" "<your-jwt-signing-key>"
dotnet user-secrets set "Authentication:Google:ClientId" "<google-client-id>"
dotnet user-secrets set "Authentication:Google:ClientSecret" "<google-client-secret>"
dotnet user-secrets set "ImageKit:PublicKey" "<imagekit-public-key>"
dotnet user-secrets set "ImageKit:PrivateKey" "<imagekit-private-key>"
dotnet user-secrets set "Stripe:SecretKey" "<stripe-secret-key>"
dotnet user-secrets set "Stripe:WebhookSecret" "<stripe-webhook-secret>"
```

Then point the database at your SQL Server and run:

```bash
dotnet run
```

The API listens on `https://localhost:7188` (Swagger available in Development).

### Frontend

```bash
cd frontend
npm install
ng serve
```

The app runs on `http://localhost:4200` and expects the API at `https://localhost:7188` (see `src/app/environments/environment.ts`).

## Project structure

```
sakan/
  frontend/    Angular application (was: EM162/sakan-app)
  backend/     ASP.NET Core solution (was: tarekmohamedx/sakan-backend)
  README.md
```

## Team

Built by a five-person team. Areas below are derived from commit history:

- **Tarek Mohamed** ([@tarekmohamedx](https://github.com/tarekmohamedx)) - backend lead: project scaffolding, real-time chat (SignalR hub, chat services), the booking dual-approval workflow with live notifications, host dashboard services, API wiring
- **Eman Sameh** ([@EM162](https://github.com/EM162)) - frontend lead: UI architecture, notifications, user reviews
- **Omar Reda** - Google external login, password reset, amenities
- **Amira Mahmoud** - support tickets and complaints
- **Abdelrhman Hisham** - admin user management

## Repository history

This monorepo was merged from two original repositories, preserving full commit history (authors and dates):

- `tarekmohamedx/sakan-backend` -> `backend/`
- `EM162/sakan-app` -> `frontend/`

The original repositories are archived and point here.
