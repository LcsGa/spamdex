<script setup vapor lang="ts">
import { computed } from "vue";
import { useStorage } from "@vueuse/core";

const cards = [
  "aldrin_gorakar.webp",
  "amber.webp",
  "artisan_des_heures.webp",
  "astry.webp",
  "baleine_farceuse.webp",
  "blaze.webp",
  "bleu_mange_cailloux.webp",
  "croqueur_de_fruits_verdoyant.webp",
  "dragonnet_des_lumieres.webp",
  "eclat_du_renard_blanc.webp",
  "esprit_eau.webp",
  "esprit_feu.webp",
  "esprit_lumiere.webp",
  "esprit_nature.webp",
  "esprit_ombre.webp",
  "esprit_terre.webp",
  "faerylia.webp",
  "felin_errant.webp",
  "gardien_vert.webp",
  "girafe_florale.webp",
  "guerrier_des_neiges.webp",
  "hibernatus.webp",
  "hippocampe_nimbe.webp",
  "le_transporteur_sauvage.webp",
  "leo.webp",
];

const count = useStorage("count", 3);

function zoomIn() {
  count.value = Math.max(1, count.value - 1);
}

function zoomOut() {
  count.value += 1;
}

function getCardUrl(card: string) {
  return new URL(`./assets/${card}`, import.meta.url).href;
}
</script>

<template>
  <header class="header">
    <h1>Spamdex</h1>
  </header>

  <main class="main">
    <ul class="card-list">
      <li v-for="card in cards" :key="card" class="ui-card ui-elevated">
        <img :src="getCardUrl(card)" alt="" />
      </li>
    </ul>

    <div role="group" class="ui-button-group ui-vertical ui-tonal">
      <button class="ui-button" aria-label="Zoom in" @click="zoomIn">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-plus preview-icon"
        >
          <path d="M5 12h14" />
          <path d="M12 5v14" />
        </svg>
      </button>
      <button class="ui-button" aria-label="Zoom out" @click="zoomOut">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-minus preview-icon"
        >
          <path d="M5 12h14" />
        </svg>
      </button>
    </div>
  </main>
</template>

<style scoped>
.header,
.main {
  --gutter: var(--size-4);
  padding: var(--gutter);
}

.card-list {
  --gutters-size: calc(var(--gutter) * (v-bind("count") + 1));
  --min-size: calc((100dvw - var(--gutters-size)) / v-bind("count"));
  padding: 0;
  display: grid;
  gap: var(--gutter);
  grid-template-columns: repeat(auto-fill, minmax(min(var(--min-size), 100%), 1fr));
}

.ui-button-group {
  position: fixed;
  inset-block-end: var(--size-3);
  inset-inline-end: var(--size-3);
}
</style>
