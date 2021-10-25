<template>
    <div>
      <path-to-file :path="path" />
      <tree 
        :directory="directory" 
        @select-file="onSelectElement" 
        :selectedElement="selectedElement"
        :max-level="maxLevel"
      />
    </div>
</template>

<script>
import tree from './tree.vue'
import pathToFile from './path.vue'

export default {
  name: 'filesystem',
  components: {
    tree,
    pathToFile
  },
  props: {
    directory: {
      type: Object,
      required: true
    },
    maxLevel: {
      type: Number,
      default: -1
    }
  },
  data() {
    return {
      selectedElement: '',
      path: ''
    }
  },
  methods: {
    onSelectElement(id) {
      this.selectedElement = id

      const indexes = id.split('-')
      let current = this.directory.contents
      let path = this.directory.name
      for (let i = 1; i < indexes.length; i++) {
        path = `${path}/${current[indexes[i]].name}`
        current = current[indexes[i]].contents
      }
      
      this.path = path
    }
  }
}
</script>
