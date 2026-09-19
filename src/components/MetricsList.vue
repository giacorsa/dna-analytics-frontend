<template>
  <section>
    <h2 class="section-title">Metriche chiave</h2>
    <p class="section-subtitle">
      Clicca su una metrica per visualizzare il grafico temporale.
    </p>

    <div class="metrics-list">
      <button
        v-for="metric in metrics"
        :key="metric.key"
        class="metric-item"
        :class="{ active: metric.key === selectedKey }"
        @click="$emit('select', metric.key)"
      >
        <div class="metric-main">
          <span class="metric-label">{{ metric.label }}</span>
          <span class="metric-key">{{ metric.description }}</span>
        </div>
        <span class="metric-chevron">›</span>
      </button>
    </div>
  </section>
</template>

<script setup>
defineProps({
  metrics: {
    type: Array,
    required: true,
  },
  selectedKey: {
    type: String,
    required: true,
  },
});

defineEmits(["select"]);
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

.metrics-list {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.metric-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(21, 26, 44, 0.9);
  border-radius: 12px;
  padding: 0.6rem 0.75rem;
  border: 1px solid transparent;
  cursor: pointer;
  color: inherit;
  transition:
    border-color 0.15s ease,
    background 0.15s ease,
    transform 0.1s ease;
}

.metric-item:hover {
  border-color: rgba(79, 209, 197, 0.4);
  transform: translateY(-1px);
}

.metric-item.active {
  border-color: var(--accent);
  background: rgba(44, 122, 123, 0.35);
}

.metric-main {
  display: flex;
  flex-direction: column;
}

.metric-label {
  font-size: 0.9rem;
  font-weight: 500;
}

.metric-key {
  font-size: 0.75rem;
  color: var(--muted);
}

.metric-chevron {
  font-size: 1rem;
  color: var(--muted);
}
</style>
