<template>
  <div class="page home">
    <div class="full-width">
      <div class="logo-area">
        <span>Bright</span>
        <img :class="{ loading: isLoading }" src="@/assets/images/logo/brightbrands-star.png" />
        <span>Brands</span>
      </div> 
      <h1>Laat jouw website door ons checken!</h1>
      <div class="input-area">
        <div class="input-area">
          <input ref="inputField" v-model="input" placeholder="Typ hier je website url..." type="text" @keyup.enter="makeRequest" />
          <button @click="makeRequest">Beoordeel mijn website</button>
        </div> 
      </div>
      <div class="chat-area">
        <ChatArea :response="response"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ChatArea from '@/components/ChatArea.vue'
import axios from 'axios';

export default defineComponent({
  name: 'HomeView',
  data() {
    return {
      input: '' as string,
      response: {},
      isLoading: false,
    };
  },
  components: {
    ChatArea
  },
  methods: {
    async makeRequest() {
      console.log(this.input);
      this.isLoading = true;
      try {
        const response = await axios.post('http://localhost:3000/message', {
          inputMessage: this.input,
        });
        this.response = JSON.parse(response.data.reply.content);
        console.log(this.response);
      } catch (error) {
        console.error('Error sending chat:', error);
        console.error('Max retries reached. Giving up.');
      } finally {
        this.isLoading = false;
      }
    },
  },
});
</script>

<style lang="scss" scoped>
.page.home {
  background-color: #ffff2b;

  svg {
    width: 800px;
    margin-bottom: 30px;
  }

  .full-width {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;

    .logo-area {
      display: flex;
      gap: 35px;
      align-items: center;

      img {
        width: 55px;
        height: 55px;

        &.loading {
          animation: spin 750ms linear infinite;
        }
      }

      span {
        font-family: 'archiaregular';
        font-weight: 700;
        font-size: 5rem;
      }
    }

    .input-area {
      margin-top: 25px;
      display: flex;

      input {
        font-family: 'archiaregular';
        border: none;
        border-radius: 999px 0 0 999px;
        padding: 15px 25px 15px 25px;
        width: 500px;
        border: 1px solid black;
        background: #ffffff69;
      }

      button {
        font-family: 'archiaregular';
        padding-left: 25px;
        padding-right: 25px;
        background: black;
        border: none;
        border-radius: 0 999px 999px 0;
        color: white;
          transition: all 500ms ease;

        &:hover {
          cursor: pointer;
          background-color: #ffff2b;
          transform: translateX(15px);
          color: black;
          border: 1px solid black;
        }
      }
    }

    .logo {
      max-width: 200px;
    }
  }

  h1 {
    margin-top: 32px;
    margin-bottom: 16px;
    color: black;
    text-align: center;
    font-size: 2rem;
  }

  h2 {
    color: var(--white);
    font-weight: 200;
  }

  #star {
    //animation: loading-star 500ms infinite;
  }

  @keyframes loading-star {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(720deg);
    }
  }
  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
}
</style>
