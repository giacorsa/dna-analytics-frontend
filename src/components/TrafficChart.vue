<template>
  <section class="chart-section">
    <header class="chart-header">
      <div>
        <h2 class="chart-title">
          Andamento {{ labelForMetric }}
        </h2>
        <p class="chart-subtitle">
          Dati temporali dalla testata online DnA.
        </p>
      </div>
    </header>

    <Line
      v-if="chartConfig"
      :data="chartConfig.data"
      :options="chartConfig.options"
    />
  </section>
</template>

<script setup>
import { computed } from 'vue';
import {
  Chart as ChartJS,
  LineElement,
  PointElement,
  LinearScale,
  CategoryScale,
  Tooltip,
  Legend
} from 'chart.js';
import { Line } from 'vue-chartjs';

ChartJS.register(
  LineElement,
  PointElement,
  LinearScale,
  CategoryScale,
  Tooltip,
  Legend
);

const props = defineProps({
  metricKey: {
    type: String,
    required: true
  },
  chartData: {
    type: Object,
    required: true
  }
});

const labelForMetric = computed(() => {
  switch (props.metricKey) {
    case 'subscriptions':
      return 'delle iscrizioni';
    case 'impressions':
      return 'delle impressions';
    default:
      return '';
  }
});

const chartConfig = computed(() => {
  if (!props.chartData) return null;

  return {
    data: {
      labels: props.chartData.labels,
      datasets: [
        {
          label: labelForMetric.value,
          data: props.chartData.values,
          borderColor: '#4fd1c5',
          backgroundColor: 'rgba(79, 209, 197, 0.15)',
          tension: 0.25,
          fill: true,
          pointRadius: 3,
          pointHoverRadius: 5
        }
      ]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: {
          labels: {
            color: '#e2e8f0'
          }
        },
        tooltip: {
          callbacks: {
            label: (ctx) => ` ${ctx.parsed.y}`
          }
        }
      },
      scales: {
        x: {
          ticks: {
            color: '#a0aec0'
          },
          grid: {
            color: 'rgba(255, 255, 255, 0.04)'
          }
        },
        y: {
          ticks: {
            color: '#a0aec0'
          },
          grid: {
            color: 'rgba(255, 255, 255, 0.04)'
          }
        }
      }
    }
  };
});
</script>

<style scoped>
.chart-section {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.chart-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 0.75rem;
}

.chart-title {
  font-size: 1rem;
  font-weight: 600;
}

.chart-subtitle {
  font-size: 0.8rem;
  color: var(--muted);
}

.chart-section :deep(canvas) {
  max-height: 380px;
}
</style>
