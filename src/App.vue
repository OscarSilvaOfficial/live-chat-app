<template>
  <div id="app">
    <div v-for="data in globalMessages" :key="data.id">
      <Message :name="data.name" :message="data.message" />
    </div>
    <form>
      <v-text-field
        class="inputText"
        v-model="userName"
        label="Nome"
        solo
      ></v-text-field>
      <v-text-field
        class="inputText"
        v-model="userMessage"
        label="Mensagem"
        solo
      ></v-text-field>
      <v-btn @click="submitForm()">Enviar</v-btn>
    </form>
  </div>
</template>

<script>
import { io } from "socket.io-client";
import Message from "./components/Message";

const socketIo = io("http://localhost:5000");

export default {
  name: "App",

  components: {
    Message,
  },

  mounted() {
    socketIo.on("receivedMessage", (messages) => {
      this.pushMessage(messages);
    });
  },

  data() {
    return {
      userName: "",
      userMessage: "",
      globalMessages: [],
    };
  },

  methods: {
    pushMessage(message) {
      this.globalMessages.push(message);
    },

    submitForm() {
      const messageData = {
        name: this.userName,
        message: this.userMessage,
      };

      socketIo.emit("sendMessage", messageData);

      this.globalMessages.push(messageData);
    },
  },
};
</script>
<style lang="scss" scope>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Montserrat;
  margin-top: 1rem;

  form {
    display: flex;
    flex-direction: column;
    max-width: 800px;
    width: 100%;

    button {
      margin: 8px 0 0;
      background: rgb(92 187 246);
      font-weight: 600;
    }
  }
}
</style>
