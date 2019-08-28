<template>
  <div id="app">
    <div id="join">
      <h1>Join a video session</h1>
      <form @submit.prevent="joinSession">
        <p>
          <label>Session:</label>
          <input type="text" id="sessionId" value="SessionA" required />
        </p>
        <p>
          <input type="submit" value="JOIN" />
        </p>
      </form>
    </div>

    <div id="session">
      <h1 id="session-header"></h1>
      <input type="button" @click="leaveSession" value="LEAVE" />
      <div>
        <div id="publisher" ref="publisher"><h3>YOU</h3></div>
        <div id="subscriber"><h3>OTHERS</h3></div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { getToken, joinSession, leaveSession } from "./app";

export default {
  name: "app",
  methods: {
    async joinSession() {
      try {
        const session = await joinSession(this.$refs.publisher);
      } catch (error) {
        console.error(error);
      }
    },
    leaveSession() {
      leaveSession();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.session {
  display: block;
}
</style>
