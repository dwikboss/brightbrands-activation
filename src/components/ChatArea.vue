<template>
  <div class="full-width">
    <div class="chat-area">
      <div class="chat-messages">
        <div class="status-bar">BrightBrands<span class="status">Online</span></div>
        <div class="message-container">
          <div v-for="(message, name) in response" :key="name" class="message">
            <img :src="'images/' + name + '.jpeg'" alt="pfp" />
            <p class="message-content">{{ message }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'ChatArea',
  props: {
    response: {},
  },
});
</script>

<style scoped>
.full-width {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  height: 100vh;
  width: 35%;

  .chat-area {
    background-color: black;
    border: 3px solid rgb(82, 82, 82);
    border-bottom: 0;
    padding: 25px;
    border-radius: 30px 30px 0 0;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-bottom: 0px;

    .chat-messages {
      display: flex;
      flex-direction: column;
      justify-content: center;
      background: url('@/assets/images/wapp-bg.png');
      border-radius: 20px 20px 0 0;

      .message-container {
        padding: 35px;
        overflow: auto;
        max-height: 65vh;
        flex-direction: column;
        display: flex;
        gap: 25px;
      }

      .status-bar {
        padding: 20px;
        padding-left: 35px;
        background-color: #075e55;
        border-top: 25px solid #054c44;
        color: white;
        font-family: 'archiaregular';
        font-size: 1.2rem;
        display: flex;
        flex-direction: column;

        .status {
          font-size: 14px;
          color: rgb(218, 218, 218);
        }
      }
    }

    .message {
      width: 80%;
      display: flex;
      align-items: flex-end;
      gap: 10px;

      &:nth-child(even) {
        align-self: end;
        flex-direction: row-reverse;
      }

      .message-content {
        background: #f0f0f0;
        padding: 15px;
        border-radius: 10px 10px 10px 0;
        font-family: 'archiaregular';
        font-size: 14px;
      }

      img {
        height: 40px;
        width: 40px;
        border-radius: 999px;
      }
    }

    h3 {
      margin: 0;
      font-weight: bold;
    }

    p {
      margin: 5px 0 0;
    }
  }
}
</style>
