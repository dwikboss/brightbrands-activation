<template>
  <div class="page home">
    <div class="full-width">
      <h1>BrightBrands activation</h1>
      <div class="input-area">
        <div class="full-width">
          <input ref="inputField" v-model="input" placeholder="Website hier" type="text" @keyup.enter="makeRequest" />
          <button @click="makeRequest">send</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  name: 'HomeView',
  data() {
    return {
      input: '' as string,
      response: '' as string,
    };
  },
  methods: {
    async makeRequest() {
      console.log(this.input);
      try {
        const response = await axios.post('http://localhost:3000/message', {
          inputMessage: this.input,
        });
        this.response = JSON.parse(response.data.reply.choices[0].message.content);
        console.log(this.response);
      } catch (error) {
        console.error('Error sending chat:', error);
        console.error('Max retries reached. Giving up.');
      }
    },
  },
});
</script>

<style lang="scss" scoped>
.page.home {
  background-color: var(--black);
  height: 100vh;

  .full-width {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;

    .logo {
      max-width: 200px;
    }
  }

  h1 {
    margin-top: 32px;
    margin-bottom: 16px;
    color: var(--white);
    text-align: center;
  }

  h2 {
    color: var(--white);
    font-weight: 200;
  }
}
</style>
