<template>
  <div
    id="context-menu"
    v-if="show"
    v-bind:style="{ top: top + 'px', left: left + 'px' }"
  >
    <div
      class="context-menu-item"
      v-for="item in optionList"
      v-bind:key="item.name"
      v-on:click="handle_item_click(item)"
    >
      {{ item.name }}
    </div>
  </div>
</template>

<script>
export default {
  name: "ContextMenu",
  props: ["message", "optionList"],
  data() {
    return {
      left: 0, // left position
      top: 0, // top position
      show: false,
    };
  },
  watch: {
    message() {
      switch (this.message.command) {
        case "Display":
          this.open(this.message.data.top, this.message.data.left);
          break;
        case "Hide":
          this.close();
          break;
      }
    },
  },
  methods: {
    close() {
      this.show = false;
    },
    open(top, left) {
      //let target = document.querySelector("#context-menu");
      this.left = left;
      this.top = top;
      this.show = true;
    },
    handle_item_click(item) {
      console.log(item);
      this.$emit("message", {
        command: item.value,
        data: { position: { left: this.left, top: this.top } },
      });
      this.show = !item.close;
    },
  },
};
</script>

<style>
#context-menu {
  position: fixed;
  background: white;
  z-index: 999;
  outline: none;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  cursor: pointer;
}
.context-menu-item {
  padding: 4px;
  background-color: #ccddff;
  color: #445599;
}
.context-menu-item:hover {
  background-color: #445599;
  color: #ccddff;
}
</style>