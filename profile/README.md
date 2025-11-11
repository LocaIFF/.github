# 🗺️ **LocaIFF (Lugaiff)**
> Kiosk interativo para orientar alunos, visitantes e servidores no **IFF – Campus Campos Centro**.

<p align="center">
  https://github.com/SEU_USUARIO/SEU_REPO/actions
    <img alt="Build" src="https://img.shields.io/badge/build-passing-22c55e?style=hubactions&logoColor=white
  </a>
  https://vercel.com/
    <img alt="Deploy" src="https://img.shields.io/badgetyle=for-the-badge&logo=vercel&logoColor=white
  </a>
  LICENSE
    <img alt="License" src="https://img.shields.io/badge/license-MITdge
  </a>
  https://github.com/SEU_USUARIO/SEU_REPO/pulls
    <img alt="PRs" src="https://img.shields.io/badge/tyle=for-the-badge&logo=github
  </a>
</p>

---

Uma aplicação web **full-screen**, **touch-friendly**, que exibe **plantas do campus** e calcula a **rota mais curta e acessível** até o destino.

---

## 🎯 **Objetivo**

- 🧭 Ajudar quem chega ao campus a encontrar **salas, setores e serviços** rapidamente.  
- 📱 Disponibilizar um **totem/tablet** com interface simples, botões grandes e suporte a toque.  
- ♿ Exibir **rotas otimizadas**, considerando **acessibilidade**.

---

## 🚀 **Funcionalidades (MVP)**

- 🗺️ Visualização do **mapa/planta por camadas** com zoom e pan.  
- 🔍 Busca de **pontos de interesse (POIs)** com hotspots clicáveis.  
- ➡️ Exibição de **rota básica** entre origem e destino.  
- 📱 Interface **responsiva**, preparada para **modo kiosk**.

---

## 🛠️ **Stack Tecnológica**

### 🔹 **Frontend**
- ⚛️ React 18  
- 🎨 Tailwind CSS 3 (PostCSS + Autoprefixer)  
- 🤏 Interação: `react-zoom-pan-pinch` (gestos de zoom/pan/pinch)  
- 🌐 HTTP: Axios (para futura integração com API)  
- 🗺️ Mapa: imagens `.webp`/`.png` por camada (`/public/maps`) + hotspots/layers em JS  

### 🔹 **Backend** *(planejado)*
- 🟢 Node.js + Express (API REST)  
- 🧬 ORM: Prisma (ou SQL direto inicialmente)  
- 🧠 Cálculo de rotas: `pgRouting` (`pgr_dijkstra` / `pgr_astar`) ou algoritmo A* no Node (MVP)  

### 🔹 **Banco de Dados**
- 🐘 PostgreSQL + PostGIS  
- 🧭 `pgRouting` para cálculo de menor caminho  
- 📊 Tabelas:
  - `nodes` (POINT)  
  - `edges` (LINESTRING com custo)  
  - `pois` (POINT, referência a node)  
  - `buildings`, `floors`

### 🔹 **Infraestrutura / Deploy** *(sugestões)*
- 🌐 Web: Vercel (MVP)  
- 🔌 API: Render / Railway / Fly.io  
- 🗄️ DB: Supabase / Render / Aiven (com PostGIS habilitado)  
- 🖥️ Kiosk: Fully Kiosk Browser (Android)

---

## 🤝 **Qualidade e Colaboração**

- 📌 GitHub:
  - Issues
  - Projects (Kanban)
  - Pull Requests com revisão

---

## 🧱 **Arquitetura (visão rápida)**

```mermaid
graph TD
  Frontend -->|Exibe| Mapas[Camadas PNG/WEBP + Hotspots]
  Frontend -->|Chama| API
  API -->|GET| /pois & /layers
  API -->|POST| /route?from=...&to=...
  API -->|Consulta| DB[(PostgreSQL + PostGIS)]
  DB -->|Calcula rota| pgRouting
