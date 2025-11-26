<script setup>
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'
</script>
<template>
  <div class="color-list">
    <button
      v-for="color in colors"
      :key="color"
      :style="{ backgroundColor: color }"
      class="color-btn"
      @click="selectColor(color)"
    ></button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      colors: ['#ff0000', '#00ff00', '#0000ff', '#ffaa00', '#00aaff', '#ff00aa'],
      selected: null,
    }
  },
  methods: {
    selectColor(c) {
      this.selected = c
    },
  },
}
</script>

<style>
.color-btn {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  border: 2px solid #ccc;
  cursor: pointer;
}
.color-btn:hover {
  transform: scale(1.1);
}

.color-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
