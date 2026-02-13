---
theme: default
background: https://images.unsplash.com/photo-1497215728101-856f4ea42174?auto=format&fit=crop&q=80&w=2000
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## Kong API Gateway Presentation
  The Cloud-Native API Gateway & Service Mesh
drawings:
  persist: false
transition: slide-left
title: Kong API Gateway
---

# Kong API Gateway

The Cloud-Native API Gateway & Service Mesh

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-black/10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.prev" class="text-xl icon-btn opacity-50 !border-none hover:opacity-100">
    <carbon:chevron-left/>
  </button>
  <button @click="$slidev.nav.next" class="text-xl icon-btn opacity-50 !border-none hover:opacity-100">
    <carbon:chevron-right/>
  </button>
</div>

---
transition: fade-out
---

# 📋 Agenda

- **What is Kong & Why API Gateways?**
- **Kong Architecture & Core Concepts**
- **Key Features & Plugins**
- **Declarative Configuration (YAML)**
- **Deployment Models**
- **Real-World Use Cases**
- **Kong at OPEN SI**
- **Live Demo**
- **Best Practices & Q&A**

---

# 🦍 What is Kong?

### Definition
Kong is a **cloud-native, platform-agnostic, scalable API Gateway** distinguished for its high performance and extensibility via plugins.

### Technical Foundation
- Built on **Nginx** and **OpenResty** (lua-nginx-module)
- Written in **Lua** for high performance
- Open-source with enterprise offerings
- Cloud-native and Kubernetes-ready

<v-click>

> **🎯 Key Value:** Single entry point for all API traffic with centralized control for security, monitoring, and management.

</v-click>

---
layout: two-cols
---

# ❌ The Problem

### Challenges:
- **Duplicated Code:** Each service implements its own security
- **Inconsistent Policies:** Different rate limits, auth methods
- **Management Nightmare:** Update 20 services for one policy change
- **Security Risks:** One misconfigured service = breach
- **Poor Observability:** Scattered logs across services

::right::

<div class="flex justify-center items-center h-full">
  <img src="/images/no_api_gateway.png" class="rounded-lg shadow-2xl border border-black/5 w-full" />
</div>

---
layout: two-cols
---

# ✅ The Solution

### Benefits:
- **🎯 Centralized:** One place to configure all API policies
- **🔐 Secure:** Consistent authentication & authorization
- **⚡ Fast:** Caching, load balancing, rate limiting
- **📊 Observable:** Unified logging & monitoring

::right::

<div class="flex justify-center items-center h-full">
  <img src="/images/api_gateway.png" class="rounded-lg shadow-2xl border border-black/5 w-full" />
</div>

---

# 🏗️ Kong Architecture

<div class="grid grid-cols-2 gap-8 items-center">
<div>

- **Proxy Port (8000):** Handles incoming client traffic
- **Admin API (8001):** Configuration & management
- **Database:** Stores config (optional)
- **Plugin System:** Extensible functionality

<v-click>

> Designed for sub-millisecond latency.

</v-click>

</div>
<div>
  <img src="/images/internal_architecture.png" class="rounded-xl shadow-2xl border border-black/5" />
</div>
</div>

---

# 🔧 Core Concepts: Services & Routes

### 1️⃣ Service
A Service wraps properties of HTTP(s) endpoints.

```bash
# Create a service
curl -i -X POST http://localhost:8001/services \
  --data "name=user-service" \
  --data "url=http://user-api:8080"
```

### 2️⃣ Route
Routes define how incoming requests map to services.

```bash
# Create a route
curl -i -X POST http://localhost:8001/services/user-service/routes \
  --data "paths[]=/api/users" \
  --data "methods[]=GET"
```

---

# 📄 Declarative Configuration (YAML)

Manage Kong without a database using a single source of truth.

<div class="grid grid-cols-2 gap-4">
<div>

### Benefits of DB-less
- **GitOps-ready:** Store config in Git
- **Simplicity:** No database to manage
- **Performance:** Instant config loading
- **Immutable:** Ensures consistency

</div>
<div>

```yaml
_format_version: "3.0"
services:
  - name: my-service
    url: http://api.internal:8080
    routes:
      - name: my-route
        paths:
          - /api/v1
    plugins:
      - name: key-auth
      - name: rate-limiting
        config:
          minute: 100
```

</div>
</div>

---

# 🔧 Core Concepts: Consumers & Plugins

### 3️⃣ Consumer
Wraps properties of anyone using API endpoints.

```bash
# Create a consumer
curl -i -X POST http://localhost:8001/consumers \
  --data "username=john_doe"
```

### 4️⃣ Plugin
Pluggable features to enrich functionalities.

```bash
# Enable JWT authentication plugin
curl -X POST http://localhost:8001/services/user-service/plugins \
  --data "name=jwt"
```

---
layout: center
class: text-center
---

# 🔌 Kong Plugin Ecosystem

**50+ official plugins** + custom plugins in Lua or Go

<div class="grid grid-cols-3 gap-6 text-left mt-8">
  <div class="p-4 border rounded shadow-sm bg-blue-50/50 border-blue-100">
    <h4 class="text-blue-600">🔐 Auth</h4>
    <p class="text-xs opacity-70">JWT, OAuth2, API Key, Basic Auth</p>
  </div>
  <div class="p-4 border rounded shadow-sm bg-green-50/50 border-green-100">
    <h4 class="text-green-600">🛡️ Security</h4>
    <p class="text-xs opacity-70">IP Restriction, CORS, ACL, Bot Detection</p>
  </div>
  <div class="p-4 border rounded shadow-sm bg-orange-50/50 border-orange-100">
    <h4 class="text-orange-600">⚡ Traffic</h4>
    <p class="text-xs opacity-70">Rate Limit, Cache, Size Limiting</p>
  </div>
</div>

---

# 🚀 Deployment Models

| Model | Detail | Props |
|-------|--------|-------|
| **Traditional** | With DB (Postgres) | Dynamic Config, Admin API |
| **DB-less** | YAML Config | GitOps-friendly, No DB |
| **Hybrid** | CP / DP Split | High-availability enterprise |
| **K8s Native** | Ingress Controller | K8s Native management |

---

# 🚀 Deployment Models (Hybrid)

<div class="grid grid-cols-2 gap-8 items-center">
<div>

### Hybrid Mode (CP/DP)
- **Control Plane:** Manage configuration.
- **Data Plane:** Handle traffic globally.
- **Benefits:**
  - Multi-region scalability
  - Enhanced security
  - Separation of concerns

</div>
<div>
  <img src="/images/hybrid_mode.png" class="rounded-xl shadow-2xl border border-black/5" />
</div>
</div>

---

# 🔐 Key Feature: Authentication

### Example: Adding JWT Authentication

```bash {all|1-3|5-7|9-11|all}
# Step 1: Enable JWT plugin on service
curl -X POST http://localhost:8001/services/user-service/plugins \
  --data "name=jwt"

# Step 2: Create consumer with credentials
curl -X POST http://localhost:8001/consumers \
  --data "username=mobile_app"

curl -X POST http://localhost:8001/consumers/mobile_app/jwt \
  --data "key=my_jwt_key" --data "secret=my_secret"
```

---

# ⚡ Key Feature: Rate Limiting

### Protect Your APIs from Abuse

```bash
curl -X POST http://localhost:8001/services/user-service/plugins \
  --data "name=rate-limiting" \
  --data "config.minute=100" \
  --data "config.policy=local"
```

<v-click>

<div class="mt-4 p-4 bg-orange-50 border-l-4 border-orange-400 text-orange-700">
  <strong>⚠️ Important:</strong> When limit is exceeded, Kong returns HTTP 429 (Too Many Requests).
</div>

</v-click>

---

# ⚖️ Key Feature: Load Balancing

<div class="grid grid-cols-2 gap-8 items-center">
<div>

### Distribute Traffic
Kong supports sophisticated load balancing:
- **Round-robin / Weighted**
- **Least connections**
- **Consistent hashing**
- **Active/Passive Health Checks**

```bash
# Example: Add targets
curl -X POST http://localhost/.../targets \
  --data "target=api-1:8080"
```

</div>
<div>
  <img src="/images/load_balancing.png" class="rounded-xl shadow-2xl border border-black/5" />
</div>
</div>

---

# 📊 Monitoring & Observability

### Integrations:
- **📈 Prometheus:** Export metrics
- **📉 Datadog:** APM integration
- **🪵 File/HTTP Log:** Custom logging
- **🔍 Zipkin/Jaeger:** Distributed tracing

---

# 🌍 Real-World Use Cases

- **Microservices Transition**: Centralized routing for 100+ services.
- **API Monetization**: Subscription tiers with Rate Limiting.
- **Legacy Modernization**: Wrapping SOAP with REST + JWT.
- **B2B Integration**: Partner white-listing and API keys.

---
layout: center
class: text-center
---

# Kong at OPEN SI

### Standardizing our API Infrastructure

- **Centralized Management**: Unified control for all APIs.
- **Security First**: Mandatory JWT auth and protections.
- **DevOps Friendly**: CI/CD integration with decK.

---
layout: center
class: text-center
---

# 🛠️ Live Demo

1. Start Kong in DB-less mode
2. Register a mock upstream service
3. Apply Key-Auth plugin
4. Demonstrate Rate Limiting in action

---

# 🏆 Best Practices

- **Use decK/GitOps**: Avoid manual dynamic changes.
- **Stateless Data Planes**: Use Hybrid or DB-less mode.
- **Health Checks**: Enable active checks for upstreams.
- **Plugin Order**: Understand the execution lifecycle.
- **Monitoring**: Always export metrics.

---
layout: center
class: text-center
---

# Thank You!

Questions?

<div class="mt-8">
   Donald KANTI - OPEN SI<br>
  <a href="mailto:donald.kanti@opensi.com" class="text-blue-500">donald.kanti@opensi.com</a>
</div>
