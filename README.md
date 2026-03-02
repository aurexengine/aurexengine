# AurexEngine Phase 1 — “Usable by Developers” Checklist

> ⚠️ **Progress:** Only the `aurexengine/core` package has been released as **v1.0.0**. The engine is still under active development; remaining packages listed below are pending completion.


**Goal (Phase 1):** A developer can install AurexEngine (via a starter skeleton), create routes/controllers/middleware, connect to a database, authenticate users, and ship a basic web app with a working UI layer — with a clean upgrade path and minimal package conflicts.

---

## 0) Repos / Packages to exist in Phase 1

### Required packages
- `aurexengine/core`
- `aurexengine/http`
- `aurexengine/routing`
- `aurexengine/mvc`
- `aurexengine/database`
- `aurexengine/auth`
- `aurexengine/ui`
- `aurexengine/installer` *(optional name; can be inside skeleton as scripts)*
- `aurexengine/cli` *(or bundled in core if you prefer; but recommended separate)*

### Required starter app
- `aurexengine/skeleton` (Composer `create-project`)

---

## 1) Core (aurexengine/core)

### Must-have features
- **Application container**
  - Bind / singleton / resolve
  - Auto-wiring (basic constructor injection)
  - Aliases (optional but helpful)
- **Service Provider system**
  - `register()` and `boot()` lifecycle
  - Ability to add providers via config
- **Configuration**
  - Load `config/*.php`
  - Load `.env` (simple dotenv loader)
  - Cached config (optional in Phase 1)
- **Helpers & utilities**
  - `base_path()`, `config()`, `env()`, `app()`, `dd()`, `abort()`
- **Error handling**
  - Central exception handler
  - Environment-aware error output (dev vs prod)
- **Logging (minimum)**
  - File logger (daily/single)
- **Package boundaries**
  - Core does not hard-depend on feature packages (db/auth/ui) except where intentional

### Deliverables
- Unit tests for container + config loader + env loader
- Minimal documentation (install + basic usage)

### Acceptance criteria
- Skeleton can boot app and resolve services from container
- Config and env values are accessible and stable

---

## 2) HTTP (aurexengine/http)

### Must-have features
- `Request`
  - Query/body/cookies/files
  - Headers
  - Method, path, full URL
  - Input helpers (e.g., `input()`, `only()`, `has()`)
- `Response`
  - Status, headers
  - JSON response helper
  - Redirect response helper
- **Session**
  - File-based session driver (Phase 1)
- **CSRF**
  - CSRF token generation + verification middleware
- **Kernel**
  - Global middleware
  - Route middleware groups (optional but good)
  - Middleware priority support (optional)

### Deliverables
- Example middleware set: CSRF, session start, auth guard, trim strings, etc.

### Acceptance criteria
- You can create an endpoint returning HTML or JSON
- Session persists between requests
- CSRF works on POST forms

---

## 3) Routing (aurexengine/routing)

### Must-have features
- HTTP verbs: `get/post/put/patch/delete/options`
- Route params: `/users/{id}`
- Named routes
- Route groups
  - Prefix
  - Middleware
- Middleware pipeline integration
- 404 and method not allowed handling
- Route caching (optional Phase 1)

### Deliverables
- Clean route definition file format (e.g., `routes/web.php`, `routes/api.php`)

### Acceptance criteria
- A controller action can be mapped to a route
- Middleware runs in correct order
- 404/405 behave correctly

---

## 4) MVC (aurexengine/mvc)

### Must-have features
- Base `Controller`
- View rendering
  - Simple PHP view engine (Phase 1), e.g., `resources/views/*.php`
  - Layout support (basic)
- Validation (minimum viable)
  - `validate($request, rules)` with common rules: required, email, min/max, numeric, date
- Form helpers (optional)

### Deliverables
- Example pages in skeleton: home page, login page, dashboard page
- Error bag + old input support (nice-to-have)

### Acceptance criteria
- Developer can create a controller and render a view with data
- Validation errors show in UI

---

## 5) Database (aurexengine/database)

### Must-have features (Phase 1 minimum)
- Database connection manager
  - MySQL driver (required)
- Query Builder
  - select/where/order/limit/join
  - insert/update/delete
  - transactions
- Migrations
  - `migrate`, `rollback`, `status`
- Seeders
  - `db:seed`

### Optional (Phase 1 if time allows)
- Lightweight ORM/Model layer (ActiveRecord-ish)
  - `Model::find()`, `Model::where()`, `$model->save()`
- Pagination helper

### Deliverables
- Migration and seeding examples in skeleton
- `.env` DB configuration template

### Acceptance criteria
- Developer can run migrations and seed fake data
- CRUD works through builder (and model if included)

---

## 6) Auth (aurexengine/auth)

### Must-have features
- Authentication guard (session-based)
- Password hashing (bcrypt/argon2)
- Login/logout
- Auth middleware
  - `auth` (must be logged in)
  - `guest` (must be logged out)
- User provider
  - default database users table

### Optional (Phase 1 if time allows)
- Roles/permissions (simple)
- Remember-me token
- Password reset (Phase 2 candidate)

### Deliverables
- `users` table migration
- Auth controllers + views in skeleton
- `auth.php` config

### Acceptance criteria
- Developer can protect routes with `auth` middleware
- Login persists via session
- Passwords stored securely

---

## 7) Middleware (cross-package requirement)

### Must-have
- Middleware interface/contract
- Global + route middleware registration
- Common middleware shipped
  - Start session
  - Verify CSRF token
  - Auth
  - Guest
  - Trim strings / convert empty to null (optional)

### Acceptance criteria
- Middleware can be added per-route and in groups
- Errors are returned consistently (redirect vs JSON based on request type)

---

## 8) UI (aurexengine/ui)

### Must-have features
- Asset management approach
  - `public/assets` (copied/published)
  - helper like `asset('path')`
- Basic UI kit (Phase 1)
  - standard layout
  - buttons, inputs, tables, alerts
- Starter pages styled and consistent

### Important constraint (per your style)
- Use what’s already in place (e.g., jQuery UI dialogs/modals, DataTables, Chart.js) in your projects where applicable.
- Provide wrappers/helpers so developers can keep consistent UI patterns.

### Deliverables
- `/resources/views/layouts/app.php`
- `/public/assets` includes baseline JS/CSS

### Acceptance criteria
- UI components usable without framework rewrites
- Example CRUD page uses dialogs + tables + charts (optional)

---

## 9) CLI (aurexengine/cli)

### Must-have commands
- Project
  - `aurex serve` (optional; can be documented with PHP built-in server)
- Code generation
  - `aurex make:controller`
  - `aurex make:middleware`
  - `aurex make:model` (if ORM exists)
  - `aurex make:migration`
  - `aurex make:seeder`
- Database
  - `aurex migrate`
  - `aurex migrate:rollback`
  - `aurex db:seed`
- Maintenance
  - `aurex config:cache` (optional)
  - `aurex route:list` (nice-to-have)

### Acceptance criteria
- Developer can scaffold a CRUD feature with commands + minimal manual edits

---

## 10) Installer (aurexengine/installer or within skeleton)

### Must-have
- `.env` setup workflow
  - Copy `.env.example` → `.env`
- Database setup helper
  - “create DB + run migrations + seed” script (CLI-driven)
- Health check page/command
  - checks PHP version/extensions, writable paths, DB connectivity

### Acceptance criteria
- Fresh install can be running with 3–5 commands max

---

## 11) Skeleton (aurexengine/skeleton) — the real “Phase 1” product

### Must-have structure
- `public/index.php`
- `routes/web.php`, `routes/api.php`
- `config/*`
- `resources/views/*`
- `storage/*` (logs/cache/sessions)
- `bootstrap/app.php` (or equivalent)
- Example modules/pages:
  - Home
  - Auth (login/logout)
  - Dashboard (protected route)
  - Example CRUD (db + validation + UI)

### Acceptance criteria
- `composer create-project aurexengine/skeleton`
- Configure `.env`
- Run migrations + seed
- Open browser and use:
  - login
  - dashboard
  - CRUD page

---

## 12) Documentation required in Phase 1

### Must-have docs
- Installation
- Folder structure
- Routing
- Controllers + views
- Middleware
- Database + migrations + seeders
- Auth
- CLI commands reference
- Upgrade policy (SemVer + how to update)

### Acceptance criteria
- A new dev can build a small app without reading source code

---

## Phase 1 “Done” Definition (final)

Phase 1 is complete when:
- Skeleton boots cleanly and ships a small working app
- Routing + middleware + controllers + views all work
- Database migrations + seeding work
- Auth works with protected routes
- UI baseline is consistent and usable
- CLI scaffolding reduces manual boilerplate
- Docs are sufficient for first-time users

---

## Suggested Phase 2 candidates (not required now)
- Package auto-discovery (if not implemented yet)
- View components system
- Queue + jobs
- Cache drivers (redis/file)
- API auth (tokens)
- Livewire-like reactive layer (`aurexengine/livewire`)
- Full permission/role management
