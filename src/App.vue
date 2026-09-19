<template>
  <div class="app-shell">
    <aside class="card">
      <header class="app-header">
        <div>
          <h1 class="app-title">DnA Analytics</h1>
          <p class="app-subtitle">
            Monitoraggio traffico testata online
          </p>
        </div>
        <span class="badge">Dashboard beta</span>
      </header>

      <MetricsList
        :metrics="metrics"
        :selected-key="selectedMetricKey"
        @select="handleMetricSelect"
      />

      <MetricsSummary
        v-if="totals"
        class="summary"
        :totals="totals"
        :selected-key="selectedMetricKey"
      />
    </aside>

    <main class="card">
      <TrafficChart
        v-if="chartData"
        :metric-key="selectedMetricKey"
        :chart-data="chartData"
      />
      <p v-else class="app-subtitle">
        Seleziona una metrica per visualizzare l’andamento nel tempo.
      </p>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import axios from 'axios';
import MetricsList from './components/MetricsList.vue';
import MetricsSummary from './components/MetricsSummary.vue';
import TrafficChart from './components/TrafficChart.vue';

const metrics = [
  { key: 'subscriptions', label: 'Subscriptions', description: 'Numero di iscrizioni' },
  { key: 'impressions', label: 'Impressions', description: 'Visualizzazioni delle pagine' }
];

const selectedMetricKey = ref('subscriptions');
const rawData = ref(null);
const totals = ref(null);

const chartData = computed(() => {
  if (!rawData.value || !selectedMetricKey.value) return null;

  const metric = selectedMetricKey.value;
  const section = rawData.value[metric];

  if (!section || !section.data) return null;

  return {
    labels: section.data.map(entry => entry.date),
    values: section.data.map(entry => entry.value)
  };
});

const fetchData = async () => {
  try {
    const response = await axios.get('/api/metrics');
    rawData.value = response.data;

    totals.value = {
      subscriptions: rawData.value.subscriptions?.total ?? 0,
      impressions: rawData.value.impressions?.total ?? 0
    };
  } catch (error) {
    console.error('Errore nel caricamento dei dati:', error.message);
  }
};

const handleMetricSelect = (key) => {
  selectedMetricKey.value = key;
};

onMounted(() => {
  fetchData();
});
</script>

<style scoped>
.summary {
  margin-top: 1.25rem;
}
</style>
