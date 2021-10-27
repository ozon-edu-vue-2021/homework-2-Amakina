<template>
  <div
    class="directory"
    @click="onClick"
    @keyup="onKeyUp"
    tabindex="1"
  >
    <img src="../assets/directory.png" width="60" height="60" class="directory-image">
    <div>{{name}}</div>
  </div>
</template>

<script>
export default {
  name: 'directoryComponent',
  props: {
    name: {
      type: String,
      required: true
    },
  },
  methods: {
    onClick() {
      this.$emit('open-folder')
    },
    onKeyUp(key) {  
      if (key.keyCode === 13) {
        this.onClick()
      }
    }
  }
}
</script>

<style scoped>
.directory {
  display: flex;
  align-items: center;

  padding: 0.5em;
  margin-top: 1em;
  margin-bottom: 1em;
  border-radius: 5px;

  cursor: pointer;
}

.directory-image {
  margin-right: 0.5em;
}
</style>
