# DnA Analytics Dashboard

Interactive Dashboard developbed using **Vue 3 + Vite**to monitor the traffic metrics of the *DnA* scientific publication .  
This project is part of the Full Stack Developer track of the Star2Impact Master's program.

---

## 🚀 Tecnologies used

- Vue 3 (Composition API)
- Vite
- Axios
- Chart.js + vue-chartjs
- Node.js + Express (backend proxy)
- Netlify (deploy frontend)

---

## 📊 Main Features

- Metrics Visualization:
  - **Subscriptions**
  - **Impressions**
- Line chart showing the trend of the selected metric over time
- Overview of total values
- **Real‑time Simulation**: impressions increase by 5 units every 2 seconds
- Responsive Interface e dark theme

---

## 📁 Project Structure

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

backend/
 server.js
 package.json

The backend acts as a **proxy** to the public GitHub API containing the analytical data.

---

## 🔌 API used

Data comes from:

[link (https://raw.githubusercontent.com/Anita-Liberatore/dna-analytics-api/master/analytics.json) link]

The Backend esposes:

GET /api/metrics

---

## ▶️ Project start:

### Backend

cd backend
npm install
npm start

Backend available on:

http://localhost:3001

Frontend

cd frontend
npm install
npm run dev

Frontend available su:

http://localhost:5173


👨‍💻 Author

Gianni — Full Stack Developer (Star2Impact)

📄 License

MIT License

