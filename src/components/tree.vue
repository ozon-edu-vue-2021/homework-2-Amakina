<template>
  <div class="tree" :class="subtreeClass">
    <component 
      class="tree-child"
      :is="getComponentByType()" 
      :name="directory.name"
      :isSelected="isSelected"
      :style="{ zIndex: level + 1 }"
      @open-folder="onOpenFolder"
      @select-file="onSelectElement"
    />

    <div v-if="isOpen && directory.contents" >
      <div 
        v-for="(child, index) in directory.contents" 
        :key="`directory-${id + index}`"
      >
        <tree 
          :directory="child" 
          :id="`${id}-${index}`" 
          :selectedElement="selectedElement"
          :level="level + 1"
          :max-level="maxLevel"
          @select-file="onSelectElement" 
        />
      </div>
      <div class="level" :style="{ background: levelColor, zIndex: level }"></div>
    </div>
  </div>
</template>

<script>
import directoryComponent from './directory.vue'
import fileComponent from './file.vue'
import linkComponent from './link.vue'

export default {
  name: 'tree',
  components: {
    directoryComponent,
    fileComponent,
    linkComponent
  },
  props: {
    directory: {
      type: Object,
      required: true
    },
    id: {
      type: String,
      default: '0'
    },
    selectedElement: {
      type: String,
      default: ''
    },
    level: {
      type: Number,
      default: 0,
    },
    maxLevel: {
      type: Number,
      default: -1
    }
  },
  data() {
    return {
      isOpen: false
    }
  },
  computed: {
    isSelected() {
      return this.id === this.selectedElement
    },
    levelColor() {
      return '#' + Math.floor(Math.random()*16777215).toString(16);
    },
    subtreeClass() {
      return this.level > 0 && !(this.maxLevel >= 0 && this.level > this.maxLevel) 
        ? 'subtree' 
        : ''
    }
  },
  methods: {
    getComponentByType() {
      switch(this.directory.type) {
        case 'directory': return 'directoryComponent'
        case 'link': return 'linkComponent'
        default: return 'fileComponent'
      }
    },
    onOpenFolder() {
      this.isOpen = !this.isOpen
    },
    onSelectElement(id) {
      this.$emit('select-file', id || this.id)
    },
  }
}
</script>

<style scoped>
.tree {
  position: relative;
}
.tree-child {
  position: relative;
}
.subtree {
  margin-left: 60px;
}
.level {
  position: absolute;
  top: 60px;
  left: 35px;

  height: calc(100% - 80px);
  width: 3px;

  background: #e4e4e4;
}
</style>
