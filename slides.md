---
theme: default
layout: cover
background: https://images.unsplash.com/photo-1550751827-4bd374c3f58b?auto=format&fit=crop&q=80&w=2000
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## Présentation Kong API Gateway
  Le Gateway API Cloud-Native et Service Mesh
drawings:
  persist: false
transition: slide-left
title: Découverte de Kong
author: Donald KANTI - OPEN SI
favicon: /favicon.png
---

# Découverte de Kong

<div class="abs-tl m-10">
  <img src="/images/kong.svg" class="h-10 brightness-0 invert" alt="Kong Logo" />
</div>

<div class="mt-4 text-xl opacity-90">
  L'API Gateway Cloud-Native & Service Mesh
</div>

<div class="mt-20">
  <div class="font-bold text-2xl mb-2">Donald KANTI</div>
  <div class="opacity-80 text-lg">Développeur Backend @ OPEN SI</div>
</div>

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-6 py-3 rounded-full border-2 border-white/30 cursor-pointer hover:bg-white/10 transition-all duration-300">
    Commencer la présentation <carbon:arrow-right class="inline ml-2"/>
  </span>
</div>

<div class="abs-br m-10 flex items-center gap-3">
  <div class="h-10 w-auto">
    <svg id="bf42ebe0-2773-4fe8-baba-95df3bb1cab0" data-name="Calque 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 424.2 149.56" class="h-full w-auto">
      <path d="M76.7.07A74.26,74.26,0,0,0,3.43,49.91C3.45,50,8,66,20.39,85.15A54.22,54.22,0,1,1,60.91,127a129.28,129.28,0,0,0,37.51,17.17h0c30.3-8.31,47.94-33.79,49.33-66.86A74.23,74.23,0,0,0,76.7.07Z" style="fill:#ffffff"></path>
      <path d="M2,53.86s21.09,70.79,93.25,92.56c0,0-36.2,14-70.73-17S2,53.86,2,53.86Z" style="fill:#ffffff"></path>
      <path d="M159.45,114.37a1.84,1.84,0,0,1-.54-1.36V47.35a1.86,1.86,0,0,1,1.9-1.91h5.9a1.86,1.86,0,0,1,1.9,1.91v4.08a15.64,15.64,0,0,1,5.85-5.35,16,16,0,0,1,7.48-1.82,19,19,0,0,1,10,2.86,21.31,21.31,0,0,1,7.43,7.66,20.37,20.37,0,0,1,2.77,10.34V77.73a20.67,20.67,0,0,1-2.72,10.34,21,21,0,0,1-7.35,7.67,19,19,0,0,1-10.16,2.85,15.75,15.75,0,0,1-6.48-1.4,18.28,18.28,0,0,1-5.67-4V113a1.86,1.86,0,0,1-1.9,1.91h-7.08A1.82,1.82,0,0,1,159.45,114.37ZM188.16,85a10.33,10.33,0,0,0,3.13-7.57V65.4a10.69,10.69,0,0,0-10.71-10.71A10.5,10.5,0,0,0,173,57.82a10.27,10.27,0,0,0-3.17,7.58V77.46A10.25,10.25,0,0,0,173,85a10.47,10.47,0,0,0,7.62,3.13A10.31,10.31,0,0,0,188.16,85Z" style="fill:#ffffff"></path>
      <path d="M223.89,94.51a21.73,21.73,0,0,1-10.75-18.77v-9.8a21.19,21.19,0,0,1,2.91-10.88,21.42,21.42,0,0,1,7.84-7.89,21.64,21.64,0,0,1,21.68,0,21.5,21.5,0,0,1,7.84,7.89,21.18,21.18,0,0,1,2.9,10.88V72a3.88,3.88,0,0,1-3.89,3.9H224v.45a10.69,10.69,0,0,0,10.7,10.7h14.42a1.81,1.81,0,0,1,1.36.55,1.84,1.84,0,0,1,.54,1.36v6.53a1.85,1.85,0,0,1-1.9,1.9H234.73A21,21,0,0,1,223.89,94.51ZM21.54-28.39v-.81a10.7,10.7,0,1,0-21.4,0v.81Z" style="fill:#ffffff"></path>
      <path d="M268.65,96.87a1.85,1.85,0,0,1-.54-1.36V47.35a1.86,1.86,0,0,1,1.9-1.91h7.07A1.86,1.86,0,0,1,279,47.35v4.26a18.85,18.85,0,0,1,6-5.41,15.45,15.45,0,0,1,7.66-2,17.89,17.89,0,0,1,9.3,2.45,17.41,17.41,0,0,1,6.49,6.8,20.28,20.28,0,0,1,2.35,9.8v32.2a1.85,1.85,0,0,1-1.9,1.9h-7.07a1.86,1.86,0,0,1-1.91-1.9V64.67c0-3.2-.82-5.67-2.45-7.39a9,9,0,0,0-6.89-2.59,10.8,10.8,0,0,0-8.48,3.59Q279,61.67,279,67.75V95.51a1.85,1.85,0,0,1-.54,1.36,1.88,1.88,0,0,1-1.37.54H270A1.85,1.85,0,0,1,268.65,96.87Z" style="fill:#ffffff"></path>
      <path d="M353.59,96.91a34.82,34.82,0,0,1-8.85-4.39,1.52,1.52,0,0,1-.63-1,1.69,1.69,0,0,1,.09-1.22l3.17-5.72a1.82,1.82,0,0,1,1.73-1.08,2.74,2.74,0,0,1,1.36.36q6.8,4.26,12.7,4.26a11.47,11.47,0,0,0,7.57-2.31,7.49,7.49,0,0,0,2.76-6,6.32,6.32,0,0,0-1.36-4.13,11.23,11.23,0,0,0-3.62-2.86c-1.52-.78-3.72-1.75-6.62-2.90l-2.63-1.09a33.67,33.67,0,0,1-10.39-6.71q-4.22-4.08-4.22-12a19,19,0,0,1,2.5-9.8,17.23,17.23,0,0,1,6.94-6.62,21.52,21.52,0,0,1,10.24-2.36A30,30,0,0,1,373.9,33a30.59,30.59,0,0,1,8.57,4.4,1.47,1.47,0,0,1,.64,1,1.71,1.71,0,0,1-.09,1.23l-3,5.71a1.81,1.81,0,0,1-1.73,1.09,2.71,2.71,0,0,1-1.36-.36,28.32,28.32,0,0,0-6.76-3.27,19.82,19.82,0,0,0-5.75-1A9,9,0,0,0,358,44a7.42,7.42,0,0,0-2.36,5.67,7.54,7.54,0,0,0,2.58,5.85,30.24,30.24,0,0,0,8.3,4.67q.83.27,6.21,2.49a19.79,19.79,0,0,1,8.58,6.49,16.4,16.4,0,0,1,3.17,10.06,18.83,18.83,0,0,1-2.68,10,18.11,18.11,0,0,1-7.48,6.85,23.92,23.92,0,0,1-11.06,2.45A30.28,30.28,0,0,1,353.59,96.91Z" style="fill:#ffffff"></path>
      <path d="M394.45,96.87a1.82,1.82,0,0,1-.55-1.36V89.25a1.86,1.86,0,0,1,1.91-1.9h7.71V42.63h-7.71a1.86,1.86,0,0,1-1.91-1.9V34.47a1.88,1.88,0,0,1,1.91-1.91h26.48a1.81,1.81,0,0,1,1.36.55,1.85,1.85,0,0,1,.55,1.36v6.26a1.88,1.88,0,0,1-.55,1.36,1.84,1.84,0,0,1-1.36.54h-3.71V87.38h7.71a1.84,1.84,0,0,1,1.36.54,1.86,1.86,0,0,1,.55,1.36v6.26a1.86,1.86,0,0,1-.55,1.36,1.84,1.84,0,0,1-1.36.54H395.81A1.84,1.84,0,0,1,394.45,96.87Z" style="fill:#ffffff"></path>
    </svg>
  </div>
</div>

<style>
.slidev-layout.cover {
  background-color: #DE4815 !important;
  color: white !important;
  background-image: none !important;
}
.slidev-layout.cover h1 {
  color: white !important;
  font-family: sans-serif !important;
  font-weight: 900 !important;
  text-transform: uppercase;
  letter-spacing: 2px;
}
</style>

---
layout: two-cols
---

# ❌ Le Problème

### Défis :
- **Code Dupliqué :** Chaque service implémente sa propre sécurité
- **Politiques Incohérentes :** Différents limites de débit, méthodes d'auth
- **Cauchemar de Gestion :** Mettre à jour 20 services pour une seule modif
- **Risques de Sécurité :** Un service mal configuré = faille
- **Faible Observabilité :** Journaux dispersés

::right::

<div class="flex justify-center items-center h-full">
  <img src="/images/no_api_gateway.png" class="rounded-lg shadow-2xl border border-black/5 w-full" />
</div>

---
layout: two-cols
---

# ✅ La Solution

### Avantages :
- **🎯 Centralisé :** Un seul endroit pour toutes les politiques
- **🔐 Sécurisé :** Authentification et autorisation cohérentes
- **⚡ Rapide :** Caching, équilibrage de charge, limitation de débit
- **📊 Observable :** Journaux et surveillance unifiés

::right::

<div class="flex justify-center items-center h-full">
  <img src="/images/api_gateway.png" class="rounded-lg shadow-2xl border border-black/5 w-full" />
</div>

---
transition: fade-out
---

# 📋 Sommaire

- **Qu'est-ce que Kong et pourquoi un API Gateway ?**
- **Architecture de Kong & Concepts Fondamentaux**
- **Fonctionnalités Clés & Plugins**
- **Configuration Déclarative (YAML)**
- **Modèles de Déploiement**
- **Cas d'Utilisation Réels**
- **Kong chez OPEN SI**
- **Démo en Direct**
- **Bonnes Pratiques & Questions/Réponses**

---

# 🦍 Qu'est-ce que Kong ?

### Définition
Kong est un **API Gateway cloud-native, agnostique vis-à-vis de la plateforme et évolutif**.

### Fondations Techniques
- Basé sur **Nginx** et **OpenResty**
- Écrit en **Lua** pour des performances optimales
- Open-source avec des offres entreprise
- Prêt pour le cloud et Kubernetes

<v-click>

> **🎯 Valeur Clé :** Point d'entrée unique pour tout le trafic API avec un contrôle centralisé.

</v-click>

---
layout: two-cols
---

# 🏗️ Architecture de Kong

<div class="grid grid-cols-2 gap-8 items-center">
<div>

- **Port Proxy (8000) :** Trafic entrant
- **API d'Admin (8001) :** Gestion de la config
- **Base de données :** Stockage PostgreSQL (optionnel)
- **Système de Plugins :** Extensibilité complète

<v-click>

> Latence ultra-faible < 1ms.

</v-click>

</div>
<div>
  <img src="/images/internal_architecture.png" class="rounded-xl shadow-2xl border border-black/5" />
</div>
</div>

---

# 📄 Configuration Déclarative (YAML)

Source de vérité unique pour votre infrastructure.

<div class="grid grid-cols-2 gap-4">
<div>

### Avantages du DB-less
- **GitOps :** Versioning de la configuration
- **Simplicité :** Pas de DB à maintenir
- **Performance :** Rechargement instantané
- **Immuabilité :** Stabilité garantie

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

# 🔧 Concepts de Base

### 1️⃣ Service
Représente vos API cibles (amont).

### 2️⃣ Route
Définit les points d'entrée (chemins, hôtes).

### 3️⃣ Consumer
Identifie les demandeurs (utilisateurs, clients).

### 4️⃣ Plugin
Logique appliquée (Auth, Cache, Log).

---

# 🌐 Orchestration Polyglotte

Kong unifie l'architecture microservices, peu importe la stack technologique.

<div class="relative mt-8">
  <!-- Gateway Layer (Now Top) -->
  <div class="bg-gradient-to-r from-purple-900/50 to-blue-900/50 p-6 rounded-xl border border-white/10 shadow-2xl backdrop-blur relative z-10 mx-10 mb-8">
    <div class="flex items-center justify-between px-8">
      <div class="flex items-center gap-4">
        <img src="/images/kong.svg" class="h-16 w-auto brightness-0 invert" />
        <div class="text-left">
          <div class="text-2xl font-bold">Kong API Gateway</div>
          <div class="text-sm opacity-70">Unified Interface</div>
        </div>
      </div>
      <div class="flex gap-2">
        <span class="px-2 py-1 bg-white/10 rounded text-xs">Auth</span>
        <span class="px-2 py-1 bg-white/10 rounded text-xs">Rate Limit</span>
        <span class="px-2 py-1 bg-white/10 rounded text-xs">Logging</span>
      </div>
    </div>
  </div>

  <!-- Connection Lines -->
  <div class="w-full flex justify-center text-gray-500/30 text-4xl mb-4">
    ⬇️ ⬇️ ⬇️ ⬇️
  </div>

  <!-- Services Layer (Now Bottom) -->
  <div class="grid grid-cols-4 gap-4">
    <div class="flex flex-col items-center p-4 bg-green-500/10 rounded-lg border border-green-500/20">
      <logos-nodejs-icon class="text-4xl mb-2" />
      <span class="font-bold text-green-400">User API</span>
      <span class="text-xs opacity-60">Node.js</span>
    </div>
    <div class="flex flex-col items-center p-4 bg-blue-500/10 rounded-lg border border-blue-500/20">
      <logos-go class="text-4xl mb-2" />
      <span class="font-bold text-blue-400">Billing</span>
      <span class="text-xs opacity-60">Golang</span>
    </div>
    <div class="flex flex-col items-center p-4 bg-yellow-500/10 rounded-lg border border-yellow-500/20">
      <logos-python class="text-4xl mb-2" />
      <span class="font-bold text-yellow-400">ML Engine</span>
      <span class="text-xs opacity-60">Python</span>
    </div>
    <div class="flex flex-col items-center p-4 bg-red-500/10 rounded-lg border border-red-500/20">
      <logos-java class="text-4xl mb-2" />
      <span class="font-bold text-red-400">Legacy</span>
      <span class="text-xs opacity-60">Java</span>
    </div>
  </div>
  
  <div class="text-center mt-6 opacity-60 text-sm">
    Les services hétérogènes sont exposés via une façade unique.
  </div>
</div>

---
layout: center
class: text-center
---

# 🔌 Écosystème de Plugins Kong

**50+ plugins officiels** + plugins Lua ou Go sur mesure

<div class="grid grid-cols-3 gap-6 text-left mt-8">
  <div class="p-4 border rounded shadow-sm bg-blue-50/10 border-blue-200">
    <h4 class="text-blue-600">🔐 Auth</h4>
    <p class="text-xs opacity-70">JWT, OAuth2, Clé API, Basic</p>
  </div>
  <div class="p-4 border rounded shadow-sm bg-green-50/10 border-green-200">
    <h4 class="text-green-600">🛡️ Sécurité</h4>
    <p class="text-xs opacity-70">IP Restriction, CORS, ACL, Bot Detection</p>
  </div>
  <div class="p-4 border rounded shadow-sm bg-orange-50/10 border-orange-200">
    <h4 class="text-orange-600">⚡ Trafic</h4>
    <p class="text-xs opacity-70">Rate Limit, Cache, Timeout</p>
  </div>
</div>

---

# 🚀 Déploiement

| Modèle | Détails | Usage |
|-------|-------|-------|
| **Traditionnel** | Avec Postgres | Changements dynamiques |
| **DB-less** | Mode YAML | CI/CD, Dev |
| **Hybride** | Split CP / DP | Entreprise massive |
| **K8s** | Ingress Controller | Environnement Kubernetes |

---

# 🚀 Mode Hybride (CP/DP)

<div class="grid grid-cols-2 gap-8 items-center">
<div>

- **CP (Control Plane) :** Gestion centralisée.
- **DP (Data Plane) :** Noeuds stateless traitant le trafic.
- **Sécurité :** Pas de base de données exposée sur les DP.
- **Scalabilité :** Déploiement global facilité.

</div>
<div>
  <img src="/images/hybrid_mode.png" class="rounded-xl shadow-2xl border border-white/5" />
</div>
</div>

---

# ⚖️ Équilibrage de Charge

<div class="grid grid-cols-2 gap-8 items-center">
<div>

- **Algorithmes :** Round-robin, Weighted, Least-connections.
- **Health Checks :** Surveillance active des backends.
- **Stabilité :** Hachage cohérent pour les sessions.

</div>
<div>
  <img src="/images/load_balancing.png" class="rounded-xl shadow-2xl border border-white/5" />
</div>
</div>

---

# 📊 Monitoring & Observabilité

- **Prometheus** & **Grafana** (Métriques)
- **Datadog** (APM)
- **Zipkin** / **Jaeger** (Traçage)
- **ELK Stack** / **Splunk** (Journaux)

---

# 🌍 Cas d'Utilisation

- **Microservices** : Routage transparent.
- **SaaS** : Gestion des accès par client.
- **Legacy** : Modernisation avec JWT.
- **B2B** : Portails partenaires sécurisés.

---

# ⚡ Étude de Cas : Supabase

<div class="grid grid-cols-2 gap-8 items-center">
<div>

**Supabase**, l'alternative Open Source à Firebase, utilise Kong comme **orchestrateur central**.

### Le Rôle de Kong :
- **Gateway Unifié :** Point d'entrée unique pour tous les services.
- **Sécurité :** Gestion des JWT et ACL pour sécuriser l'accès aux données.
- **Routage :** Dirige le trafic vers PostgREST, Realtime, Storage et Auth.

</div>
<div>
  <div class="bg-black/40 p-6 rounded-xl border border-white/10 backdrop-blur-sm shadow-2xl">
    <div class="flex flex-col items-center gap-4">
      <div class="w-full text-center p-2 rounded bg-gray-700/50 text-gray-300 text-sm">Client (Web/Mobile)</div>
      <div class="text-gray-500">⬇️ HTTPS</div>
      <div class="w-full p-4 rounded bg-gradient-to-r from-green-900/40 to-green-600/20 border border-green-500/50 text-green-200 font-bold text-center shadow-lg shadow-green-900/30">
        🦍 Kong API Gateway
      </div>
      <div class="grid grid-cols-3 gap-2 w-full">
        <div class="p-2 rounded bg-blue-500/10 border border-blue-500/30 text-xs text-center text-blue-200">GoTrue<br>(Auth)</div>
        <div class="p-2 rounded bg-purple-500/10 border border-purple-500/30 text-xs text-center text-purple-200">PostgREST<br>(API)</div>
        <div class="p-2 rounded bg-yellow-500/10 border border-yellow-500/30 text-xs text-center text-yellow-200">Realtime<br>(WS)</div>
      </div>
      <div class="w-full p-3 rounded bg-indigo-600/20 border border-indigo-500/50 text-indigo-200 font-bold text-center">
        🐘 PostgreSQL
      </div>
    </div>
  </div>
</div>
</div>

---

# Kong chez OPEN SI

- **Standardisation :** Une seule passerelle pour toutes nos API.
- **Sécurité Native :** Authentification centralisée.
- **Performance :** Pas de goulot d'étranglement.

---

# 📚 Ressources & Liens

Pour aller plus loin avec Kong :

<div class="grid grid-cols-2 gap-6 mt-10">

<a href="https://konghq.com/" target="_blank" class="block p-6 rounded-xl bg-gradient-to-br from-cyan-500/10 to-blue-600/10 hover:from-cyan-500/30 hover:to-blue-600/30 border border-cyan-500/20 hover:border-cyan-400/50 transition-all duration-300 group shadow-lg hover:shadow-cyan-500/20">
  <div class="text-xl font-bold mb-3 flex items-center gap-3 text-cyan-300 group-hover:text-white transition-colors">
    <div class="p-2 bg-cyan-500/20 rounded-lg group-hover:bg-cyan-500/40 transition-colors">🦍</div>
    Site Officiel
    <carbon:arrow-up-right class="text-sm opacity-50 group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform"/>
  </div>
  <div class="text-sm opacity-70 group-hover:opacity-100 transition-opacity">Documentation, version Enterprise, et Support.</div>
</a>

<a href="https://docs.konghq.com/hub/" target="_blank" class="block p-6 rounded-xl bg-gradient-to-br from-purple-500/10 to-pink-600/10 hover:from-purple-500/30 hover:to-pink-600/30 border border-purple-500/20 hover:border-purple-400/50 transition-all duration-300 group shadow-lg hover:shadow-purple-500/20">
  <div class="text-xl font-bold mb-3 flex items-center gap-3 text-purple-300 group-hover:text-white transition-colors">
    <div class="p-2 bg-purple-500/20 rounded-lg group-hover:bg-purple-500/40 transition-colors">🧩</div>
    Kong Plugin Hub
    <carbon:arrow-up-right class="text-sm opacity-50 group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform"/>
  </div>
  <div class="text-sm opacity-70 group-hover:opacity-100 transition-opacity">Le catalogue complet des plugins officiels et communautaires.</div>
</a>

</div>

---

# 🏆 Bonnes Pratiques

1. **Privilégier le DB-less** pour le CI/CD.
2. **Utiliser decK** pour la gestion de config.
3. **Isoler les Control Planes**.
4. **Surveiller la latence** au niveau des plugins.

---
layout: center
class: text-center
---

# Merci !

Des questions ?

<div class="mt-8 text-sm opacity-60">
   Donald KANTI - OPEN SI<br>
  <a href="mailto:donald.kanti@mehriso.com" class="text-blue-500">donald.kanti@mehriso.com</a>
</div>
