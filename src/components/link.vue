<template>
  <div 
    class="link" 
    :class="{ 'selected': isSelected }"
    @click="onClick"
    @keyup="onKeyUp"
    tabindex="1"
  >
    <img src="../assets/link.png" width="60" height="60" class="link-image">
    <div>{{name}}</div>
  </div>
</template>

<script>
export default {
  name: 'linkComponent',
  props: {
    name: {
      type: String,
      required: true
    },
    isSelected: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    onClick() {
      this.$emit('select-file')
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
.link {
  display: flex;
  align-items: center;

  padding: 0.5em;
  margin-top: 1em;
  margin-bottom: 1em;
  border-radius: 5px;

  cursor: pointer;
}

.selected {
  background: #dbeaf2;
}

.link-image {
  margin-right: 0.5em;
}
</style>
