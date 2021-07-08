<template>
  <div v-on:click="targetless_click()">
    <img
      alt="Vue logo"
      src="./assets/logo.png"
      v-on:click.right="i_am_clicked($event)"
    />
  </div>
  <ContextMenu
    v-bind:message="message2ContextMenu"
    v-bind:optionList="[
        { name: 'Cut', value: 'CutComponent', close: true },
        { name: 'Copy', value: 'CopyComponent', close: true },
        { name: 'Delete', value: 'DeleteComponent', close: true },
        { name: 'Bring Front', value: 'FloatComponent', close: false },
        { name: 'Send Back', value: 'SinkComponent', close: false },
    ]"
    v-on:message="handle_incoming_message"
  />
</template>

<script>
import ContextMenu from "./components/ContextMenu";

export default {
  name: "App",
  components: {
    ContextMenu,
  },
  data() {
    return {
      showContextMenu: false,
      message2ContextMenu: {},
    };
  },
  methods: {
    i_am_clicked(e) {
      e.preventDefault();
      e.stopPropagation();
      this.message2ContextMenu = {
        command: "Display",
        data: { top: e.clientY, left: e.clientX },
      };
    },
    targetless_click() {
      this.message2ContextMenu = {
        command: "Hide",
        data: {},
      };
    },
    handle_incoming_message(message) {
      console.log("Child message");
      console.log(message);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
