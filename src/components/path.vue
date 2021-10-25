<template>
  <input class="path" :value="path" disabled>
</template>

<script>
export default {
  name: 'pathToFile',
  props: {
    path: {
      type: String,
      required: true
    }
  }
}
</script>


<style scoped>
.path {
  position: sticky;
  top: 0;
  z-index: 100000;

  display: flex;
  align-items: center;

  width: calc(100% - 2em);
  margin: 0 0.5em 0 0.5em;
  padding: 1em 0.5em;

  border: 1px solid #cfcfcf;
  border-radius: 5px;
  background: #fff;
}
</style>