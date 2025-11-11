# LocaIFF · Mapa Interativo do IFF – Campus Campos Centro

[![Tech React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)](https://react.dev)
[![Tailwind](https://img.shields.io/badge/TailwindCSS-3-38B2AC?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![License MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Aplicativo para orientar alunos, visitantes e servidores no IFF – Campus Campos Centro. Exibe o mapa do campus por camadas e calcula a rota mais curta e acessível até o destino solicitado.

---

## Objetivo
- Ajudar quem chega ao campus a encontrar salas, setores e serviços rapidamente.
- Interface simples para totem/tablet: botões grandes e suporte a toque.
- Exibir rotas otimizadas (menor caminho/custo), considerando acessibilidade.

## Funcionalidades
- Visualização do mapa/planta por camadas com zoom e pan.
- Busca de POIs (pontos de interesse) com hotspots clicáveis.
- Exibição de rota básica entre origem e destino.
- Interface responsiva, preparada para modo kiosk.

---

## Stack Tecnológica

Frontend
- React 18
- Tailwind CSS 3 (PostCSS + Autoprefixer)
- Gestos: react-zoom-pan-pinch
- HTTP: Axios (para futura API)
- Mapas: assets .webp/.png por camada (public/maps) + hotspots/layers em JS/JSON

Backend (planejado)
- Node.js + Express (API REST)
- ORM: Prisma (ou SQL direto no início)
- Rotas: pgRouting (pgr_dijkstra/pgr_astar) ou A* no Node (MVP)

Banco de Dados (planejado)
- PostgreSQL + PostGIS (geometria de nós/arestas/POIs)
- pgRouting para menor caminho
- Tabelas iniciais: 
  - nodes (POINT)
  - edges (LINESTRING com custo e acessibilidade)
  - pois (POINT, referência a node)
  - buildings, floors

Infra/Deploy
- Web (MVP): Vercel
- API: Render/Railway/Fly.io
- DB: Supabase/Render/Aiven com PostGIS habilitado
- Kiosk: Fully Kiosk Browser (Android)

---

## Arquitetura
Fluxo
1) Frontend exibe camadas do mapa (PNG/WEBP) e hotspots sobrepostos.  
2) API fornece POIs, layers e calcula rotas.  
3) DB armazena grafo do campus e metadados; pgRouting calcula menor caminho.

Endpoints (verificar)
- GET /pois
- GET /layers
- POST /route?from=:id&to=:id  → retorna geometria/steps

Estrutura (sugerida)
```
/public
  /maps
    terreo.webp
    andar-1.webp
/src
  /components
  /hooks
  /pages
  /services   # axios, endpoints
  /data       # hotspots/layers (MVP)
  /styles
```

## Como rodar (Frontend)
Pré-requisitos: Node.js LTS 18+ e npm.

```powershell
# Instalar dependências
npm install

# Ambiente de desenvolvimento
npm start

# Testes (Jest do CRA)
npm test

# Build de produção
npm run build
```

## Modo de apresentação (Kiosk)
Uitlizar o app: Fully Kiosk Browser (Android)
- Habilitar modo Kiosk/Imersivo (esconder barra de status e navegação).
- Fixar a URL do app (deploy) ou IP local.
- Ativar reload automático ao perder conexão.
- Definir timeout de inatividade para tela inicial.

---

## Acessibilidade
- Cores com contraste adequado (WCAG AA+).
- Tamanhos de toque ≥ 44px.
- Rotas acessíveis: marcar arestas com custo/impedâncias (escadas vs rampas/elevadores).
- Leitura de tela: rótulos ARIA nos botões e resultados.

---

## Contribuindo
- Use Issues e Projects (Kanban) no GitHub.
- Envie PRs com descrição clara e prints quando possível.
- Padrões: lint, testes passando e commits descritivos.

---

## Licença
MIT. Veja o arquivo LICENSE.
