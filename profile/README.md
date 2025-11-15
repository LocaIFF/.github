# LocaIFF · Mapa Interativo do IFF – Campus Campos Centro

[![Tech React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)](https://react.dev)
[![Tailwind](https://img.shields.io/badge/TailwindCSS-3-38B2AC?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![Tech SQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org)
[![License MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Aplicativo para orientar alunos, visitantes e servidores no IFF – Campus Campos Centro.  
Exibe o mapa do campus por camadas, mostra pontos de interesse (POIs) e, no MVP atual, simula a rota entre origem e destino no próprio frontend.

> **Status do projeto**  
> - Frontend (React + Tailwind + mapas em imagem): **implementado (MVP)**  
> - Rotas: **simuladas no frontend** (sem backend ainda)  
> - Backend + banco geoespacial (PostgreSQL/PostGIS + pgRouting): **planejado**

---

## Objetivo

- Ajudar quem chega ao campus a encontrar salas, setores e serviços rapidamente.
- Interface simples para totem/tablet: botões grandes e suporte a toque.
- Exibir rotas otimizadas (menor caminho/custo), considerando acessibilidade (planejado).

---

## Funcionalidades

### Implementadas (MVP)

- Visualização do mapa/planta por camadas com zoom e pan.
- Exibição de plantas em imagem (`.png/.webp`) por andar.
- Hotspots (POIs) clicáveis sobre o mapa.
- Busca de pontos de interesse por texto.
- Desenho de uma rota **simulada** entre origem e destino (gerada no frontend).
- Interface responsiva, preparada para uso em modo kiosk/PWA.

### Planejadas

- Cálculo de rota real no backend (pgRouting ou A*).
- Diferentes perfis de rota (menor distância, mais acessível).
- Persistência de POIs, nós e arestas em banco geoespacial.

---

## Stack Tecnológica

### Frontend (implementado)

- **React 18**
- **Create React App** (CRA) como base do projeto.
- **Tailwind CSS 3** (com PostCSS + Autoprefixer).
- **Gestos / Zoom / Pan:**  
  - [`react-zoom-pan-pinch`](https://github.com/prc5/react-zoom-pan-pinch)
- **HTTP (para futura API):**  
  - [`axios`](https://axios-http.com)  
    - Hoje usado com funções mockadas em `src/api.js`.
- **Mapas:**  
  - Assets de imagem (`.png/.webp`) por camada/andar em `public/maps`.
  - Hotspots e layers definidos em arquivos JS/JSON em `src/data`.

### Backend (planejado – ainda não implementado)

- **Node.js + Express** (API REST).
- **ORM:** Prisma (ou SQL direto no início).
- **Algoritmos de rota:**
  - `pgRouting` (`pgr_dijkstra`, `pgr_astar`) **ou**
  - Algoritmo A* implementado no Node.js (MVP de backend).

### Banco de Dados (planejado – ainda não implementado)

- **PostgreSQL + PostGIS** para suportar geometria:
  - Grafo de navegação do campus:
    - `nodes` (POINT)
    - `edges` (LINESTRING com custo e acessibilidade)
  - Pontos de interesse:
    - `pois` (POINT, referência a `node`)
  - Metadados:
    - `buildings`, `floors`
- **pgRouting** para cálculo de menor caminho/rota acessível.

### Infra / Deploy (planejado)

- **Web (MVP):** Vercel (deploy do frontend React).
- **API:** Render / Railway / Fly.io.
- **Banco de dados:** Supabase / Render / Aiven com PostGIS habilitado.
- **Kiosk (tablet/totem Android):**  
  - Fully Kiosk Browser (modo imersivo com URL travada).

---

## Arquitetura

### Fluxo (visão futura)

1. **Frontend** exibe camadas do mapa (imagens PNG/WEBP) e hotspots sobrepostos.
2. **API** fornece dados de POIs, layers e calcula rotas.
3. **Banco geoespacial** armazena grafo do campus e metadados; `pgRouting` calcula o menor caminho.

### Estado atual (MVP sem backend)

- POIs, layers e rotas são carregados/gerados diretamente no frontend:
  - `src/data/hotspots.js`
  - `src/data/layers.js`
  - `src/api.js` (funções mockadas de rota)
- A rota exibida é **simulada**: não há cálculo real em banco de dados.

### Endpoints (planejados)

Estes endpoints ainda **não existem** no repositório. São apenas o desenho da API futura:

- `GET /pois`  
  Retorna lista de pontos de interesse (salas, setores, etc.).

- `GET /layers`  
  Retorna as camadas do mapa (andares, plantas, etc.) e suas imagens.

- `POST /route?from=:id&to=:id`  
  Recebe origem e destino (ids de POI ou nó) e retorna geometria/steps da rota.

---

## Estrutura do Projeto

### Estrutura atual (MVP)

```text
/public
  /maps
    terreo.png
    andar1.png
    ...
  index.html
  manifest.json
  service-worker.js

/src
  /components
    MapViewer.jsx
    ...
  /data
    hotspots.js
    layers.js
    ...
  /utils
    routeUtils.js
    ...
  api.js
  App.jsx
  index.jsx

package.json
tailwind.config.js
postcss.config.js
README.md
```

### Estrutura futura (sugerida)

```text
/src
  /components
  /hooks
  /pages
  /services   # axios e integração com API real
  /data       # hotspots/layers (MVP ou fallback)
  /styles
  /utils
```

---

## Como rodar (Frontend)

**Pré-requisitos:**

- Node.js LTS 18+  
- npm (ou yarn, se preferir adaptar os comandos)

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

O aplicativo será servido em modo desenvolvimento, normalmente em:  
`http://localhost:3000`

---

## Modo de apresentação (Kiosk)

Sugestão de uso em totem/tablet Android com **Fully Kiosk Browser**:

1. Definir a URL do app (deploy em produção ou IP local da máquina de desenvolvimento).
2. Habilitar modo Kiosk/Imersivo (esconder barra de status e navegação).
3. Ativar reload automático ao perder conexão.
4. Definir um timeout de inatividade para voltar à tela inicial.
5. Manter o dispositivo travado apenas no app do navegador kiosk.

---

## Acessibilidade (planejada / em evolução)

- Paleta de cores com contraste adequado (WCAG AA+).
- Tamanhos de alvo de toque ≥ 44px.
- Rotas acessíveis:
  - Marcar arestas com custo/impedâncias (escadas vs rampas/elevadores).
  - Diferenciar tipos de percurso por usuário (cadeirante, etc.).
- Suporte a leitores de tela:
  - Rótulos ARIA nos botões, campos de busca e resultados.

---

## Contribuindo

1. Abra uma **Issue** descrevendo o problema/feature.
2. Opcionalmente, use o **Projects** (Kanban) do GitHub para organizar tarefas.
3. Envie **Pull Requests** com:
   - Descrição clara do que foi feito.
   - Prints ou GIFs, quando alterar a interface.
4. Padrões recomendados:
   - Lint sem erros.
   - Testes passando.
   - Commits descritivos (em português ou inglês, mas consistentes).

---

## Licença

Este projeto é licenciado sob a licença **MIT**.  
Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
