<template>
  <section>
    <h2 class="section-title">Panoramica</h2>
    <p class="section-subtitle">
      Totali aggregati e simulazione traffico in tempo reale.
    </p>

    <div class="metrics-grid">
      <div class="summary-card">
        <span class="summary-label">Subscriptions</span>
        <span class="summary-value">
          {{ totals.subscriptions }}
        </span>
      </div>

      <div class="summary-card">
        <span class="summary-label">Impressions (live)</span>
        <span class="summary-value live">
          {{ liveImpressions }}
        </span>
        <span class="summary-hint">
          +5 ogni 2s (simulazione)
        </span>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
  totals: {
    type: Object,
    required: true
  },
  selectedKey: {
    type: String,
    required: true
  }
});

const liveImpressions = ref(0);
let timerId = null;

const startSimulation = () => {
  liveImpressions.value = props.totals.impressions ?? 0;

  if (timerId) clearInterval(timerId);

  timerId = setInterval(() => {
    liveImpressions.value += 5;
  }, 2000);
};

watch(
  () => props.totals,
  () => startSimulation(),
  { immediate: true }
);

onMounted(() => startSimulation());

onBeforeUnmount(() => {
  if (timerId) clearInterval(timerId);
});
</script>

<style scoped>
.section-title {
  font-size: 0.95rem;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.section-subtitle {
  font-size: 0.8rem;
  color: var(--muted);
  margin-bottom: 0.75rem;
}

.metrics-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.75rem;
}

.summary-card {
  background: rgba(15, 20, 35, 0.95);
  border-radius: 12px;
  padding: 0.75rem;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  border: 1px solid rgba(255, 255, 255, 0.04);
}

.summary-label {
  font-size: 0.8rem;
  color: var(--muted);
}

.summary-value {
  font-size: 1.1rem;
  font-weight: 600;
}

.summary-value.live {
  color: var(--accent);
}

.summary-hint {
  font-size: 0.7rem;
  color: var(--muted);
}
</style>
