<script setup>
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'
import mqtt from 'mqtt'
import { ref } from 'vue'

const selected = ref('')
const brokerUrl = 'ws://localhost:9001' // replace with your broker

// Options including username/password
const options = {
  username: 'Diego',
  password: '0701pyja',
}

const colors = [
  '#ff0000',
  '#00ff00',
  '#0000ff',
  '#ffaa00',
  '#00aaff',
  '#ff00aa',
  '#000000',
  '#FFC896',
]
const client = mqtt.connect(brokerUrl, options)
client.on('connect', () => {
  console.log('Connected to MQTT broker')
})

client.subscribe('testTopic/color', (err) => {
  if (!err) {
    console.log('Subscribed to testTopic/color')
  }
})

function selectColor(c) {
  const map = {
    '#ff0000': 'Red',
    '#00ff00': 'Green',
    '#0000ff': 'Blue',
    '#ffaa00': 'Orange',
    '#00aaff': 'Cyan',
    '#ff00aa': 'Magenta',
    '#000000': 'Black',
    '#FFC896': 'Room',
  }
  selected.value = map[c] ?? 'Unknown'

  console.log('Selected color:', selected.value)
  client.publish('testTopic/color', selected.value)
}
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
