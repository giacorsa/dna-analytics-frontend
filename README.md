# DnA Analytics Dashboard

Dashboard interattiva sviluppata in **Vue 3 + Vite** per monitorare le metriche di traffico della testata scientifica *DnA*.  
Il progetto fa parte del percorso Full Stack Developer del Master Star2Impact.

---

## 🚀 Tecnologie utilizzate

- Vue 3 (Composition API)
- Vite
- Axios
- Chart.js + vue-chartjs
- Node.js + Express (backend proxy)
- Netlify (deploy frontend)

---

## 📊 Funzionalità principali

- Visualizzazione delle metriche:
  - **Subscriptions**
  - **Impressions**
- Grafico a linee con andamento temporale della metrica selezionata
- Panoramica dei valori totali
- **Simulazione real‑time**: le impressions aumentano di 5 unità ogni 2 secondi
- Interfaccia responsive e dark theme

---

## 📁 Struttura del progetto

### Frontend (Vue + Vite)

```text
frontend/
 index.html
 vite.config.js
 package.json
 /src
   main.js
   App.vue
   /components
      MetricsList.vue
      MetricsSummary.vue
      TrafficChart.vue

### Backend (Node.js + Express)

```text
backend/
 server.js
 package.json

```text
Il backend funge da **proxy** verso l’API pubblica GitHub contenente i dati analitici.

---

## 🔌 API utilizzata

I dati provengono da:

[link (https://raw.githubusercontent.com/Anita-Liberatore/dna-analytics-api/master/analytics.json) link]

```text
Il backend espone:

```text
GET /api/metrics

---

## ▶️ Avvio del progetto

### Backend

```bash
cd backend
npm install
npm start

Backend disponibile su:

http://localhost:3001

Frontend

cd frontend
npm install
npm run dev

Frontend disponibile su:

http://localhost:5173

🌐 Deploy su Netlify

Accedi a https://app.netlify.com/

Clicca Add new site → Import from Git

Seleziona il repository dna-analytics-frontend

Imposta:

Build command: npm run build

Publish directory: dist

Clicca Deploy site

👨‍💻 Autore

Gianni — Full Stack Developer (Star2Impact)

📄 Licenza

MIT License

