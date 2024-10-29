<template>
  <div class="chat-messages">
    <div v-for="(message, name) in response" :key="name" class="message">
      <h3>{{ name }}</h3>
      <p>{{ message }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'ChatArea',
  props: {
    response: {}
  },
});
</script>

<style scoped>
.chat-messages {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.message {
  background: #f0f0f0;
  padding: 15px;
  border-radius: 8px;
}

h3 {
  margin: 0;
  font-weight: bold;
}

p {
  margin: 5px 0 0;
}
</style>
