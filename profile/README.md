# LocaIFF (Lugaiff)
Kiosk interativo para orientar alunos, visitantes e servidores no IFF – Campus Campos Centro. Uma aplicação web full-screen, touch-friendly, que exibe plantas do campus e calcula a rota mais curta e acessível até o destino.

## Objetivo
- Ajudar quem chega ao campus a encontrar salas, setores e serviços rapidamente.
- Disponibilizar um totem/tablet com interface simples, botões grandes e suporte a toque.
- Exibir rotas otimizadas (menor caminho/custo), considerando acessibilidade.

## Funcionalidades (MVP)
- Visualização do mapa/planta por camadas com zoom e pan.
- Busca de pontos de interesse (POIs) com hotspots clicáveis.
- Exibição de rota básica entre origem e destino.
- Interface responsiva, preparada para modo kiosk.

## Stack Tecnológica

- Frontend (atual, em desenvolvimento)
  - React 18 (Create React App)
  - Tailwind CSS 3 (PostCSS + Autoprefixer)
  - Interação: react-zoom-pan-pinch (gestos de zoom/pan/pinch)
  - HTTP: Axios (integração com API futura)
  - Dados atuais: imagens do mapa por camada (public/maps) + hotspots/layers em JS (coordenadas percentuais)

- Backend (planejado)
  - Node.js + Express (API REST)
  - ORM: Prisma (ou SQL direto inicialmente)
  - Cálculo de rotas: pgRouting (pgr_dijkstra/pgr_astar) ou A* no Node (MVP)

- Banco de Dados (planejado)
  - PostgreSQL + PostGIS (geometria de nós/arestas/POIs)
  - pgRouting para menor caminho
  - Tabelas iniciais: nodes (POINT), edges (LINESTRING com custo), pois (POINT, referência a node), buildings/floors

- Infra/Deploy (sugestões)
  - Web: Vercel/Netlify (MVP)
  - API: Render/Railway/Fly.io
  - DB: Supabase/Render/Aiven com PostGIS habilitado
  - Kiosk: Chrome/Edge em modo kiosk (Windows) ou Fully Kiosk Browser (Android)

- Qualidade e Colaboração
  - Lint/format: ESLint + Prettier
  - Testes: Jest (CRA) + Playwright/Cypress (E2E no fluxo de rota)
  - GitHub: Issues, Projects (Kanban), Pull Requests com revisão
  - CI: GitHub Actions (lint + test + build)

## Arquitetura (visão rápida)
- Frontend exibe camadas do mapa (PNG/SVG) e hotspots.
- API fornece:
  - GET /pois, GET /layers
  - POST /route?from=…&to=… (retorna geometria/steps)
- DB armazena grafo do campus e POIs; pgRouting calcula a rota.

## Como rodar (Frontend – atual)
Pré-requisitos: Node.js LTS 18+ e npm.

```powershell
# Clonar e instalar
git clone https://github.com/DevJpLg/Lugaiff.git
cd Lugaiff
npm install

# Executar em desenvolvimento
npm start

# Rodar testes (Jest do CRA)
npm test

# Build de produção
npm run build
```

## Organização do trabalho (5 pessoas)
- Branches: main (prod), develop (integração), feature/nome-da-tarefa
- PRs: revisão obrigatória (1+ revisor), checks de CI verdes
- Issues: uma por funcionalidade/bug; labels (feature, bug, map, db, ui)
- Projects: Kanban (Backlog, Em andamento, Revisão, Pronto)
- Commits: Conventional Commits (ex.: feat: busca de POIs)
- CODEOWNERS: definir responsáveis por web, API e DB

## Diretrizes de dados de rota (MVP)
- nodes: id, name, building_id, floor, geom (POINT), accessible (bool)
- edges: id, source, target, cost, cost_accessible, geom (LINESTRING), type (hallway, stairs, elevator)
- pois: id, name, category, node_id, building_id, floor

## Licença
MIT
## Time e contato
Equipe da disciplina de Empreendedorismo e Projetos (IFF – Campos Centro).
Comunicação principal via GitHub (Issues/PRs/Projects).
