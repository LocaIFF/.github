# 🌐 LocaIFF · Mapa Interativo do IFF – Campus Campos Centro

> Aplicativo para guiar alunos, visitantes e servidores entre blocos e andares do IFF Campus Campos Centro.

<p align="center">
  <img src="https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white" alt="React">
  <img src="https://img.shields.io/badge/TailwindCSS-3-38B2AC?logo=tailwindcss&logoColor=white" alt="TailwindCSS">
  <img src="https://img.shields.io/badge/PostgreSQL%20%2B%20PostGIS-Planejado-4169E1?logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT">
</p>

---

## ✨ Destaques

| Status | Funcionalidade | Detalhes |
| --- | --- | --- |
| ✅ | Navegação multicapas | Plantas em alta resolução com zoom/pan via [`components/MapViewer`](src/components/MapViewer.js) |
| ✅ | Hotspots interativos | Pontos definidos em [`data/hotspots`](src/data/hotspots.js) com painel lateral [`components/InfoPanel`](src/components/InfoPanel.js) |
| ⚠️ | Rotas simuladas | Mock em [`api.requestRoute`](src/api.js) renderizado por [`utils/routeUtils`](src/utils/routeUtils.js) |
| 🗺️ | Busca inteligente | Campo + voz integrados ao estado global em [`App`](src/App.js) |
| 🚧 | Backend geoespacial | Planejado com PostgreSQL + PostGIS + pgRouting |

---

## 🧭 Roadmap rápido

- **Agora**: React 18 + Tailwind + assets PNG.
- **Curto prazo**: API Node/Express, rotas reais (Dijkstra/A*), persistência de POIs.
- **Médio prazo**: Perfis de rota (acessível vs. rápida), deploy kiosk com Fully Kiosk Browser.

---

## 🏗️ Arquitetura atual

- Dados estáticos: [`data/layers`](src/data/layers.js) · [`data/hotspots`](src/data/hotspots.js)
- Camada de UI: [`App`](src/App.js) controla timers, painel e rotas.
- Utilidades de rota: [`utils/routeUtils`](src/utils/routeUtils.js) (percentual → SVG/path).

---

## 🛠️ Stack

- **Base:** React 18 (CRA) + Tailwind 3 ([`tailwind.config.js`](tailwind.config.js))
- **Gestos:** `react-zoom-pan-pinch`
- **HTTP / Mock:** `axios` em [`api.js`](src/api.js)
- **Build:** `react-scripts`
- **PWA:** Manifest + Service Worker ([`public/manifest.json`](public/manifest.json), [`public/service-worker.js`](public/service-worker.js))

---

## 🚀 Como rodar

```bash
npm install
npm start       # http://localhost:3000
npm test        # Jest (CRA)
npm run build   # Produção
```

Pré-requisitos: Node.js 18+.

---

## 📟 Uso em modo kiosk

1. Publicar build (Vercel ou host local).
2. Configurar Fully Kiosk Browser: modo imersivo, reload auto e bloqueio de navegação.
3. Ajustar brilho/timeout físico para evitar burn-in.

---

## 🤝 Contribuindo

1. Abra uma Issue descrevendo bug ou feature.
2. Crie branch/pull request com descrição + screenshots (se UI).
3. Garanta lint/tests ok (`npm run lint`, `npm test`).
4. Commits descritivos (PT/EN, porém consistentes).
