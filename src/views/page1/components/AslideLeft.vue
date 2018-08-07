<template>
  <el-dropdown class="cpt-dropdown-list" trigger="click"
  :hide-on-click="false" @command="commandHandler">
    <span class="dropdown-link">{{ text }}</span>
    <el-dropdown-menu slot="dropdown" class="cpt-dropdown-list-wrap">
      <el-dropdown-item v-for="item in options" :key="item.key"
      :command="item" :class="{ active: isActive(item) }">
        {{ item.label }}
        <i v-show="isActive(item)" class="el-icon-check"></i>
      </el-dropdown-item>
    </el-dropdown-menu>
  </el-dropdown>
</template>

<script>
export default {
  props: {
    text: String,
    options: Array,
    selected: Array
  },

  mounted() {
    console.log(this.options)
  },

  methods: {
    isActive(data) {
      return this.selected.some(item => item.key === data.key)
    },

    commandHandler(data) {
      const temp = this.selected.slice()
      const index = temp.findIndex(item => item.key === data.key)
      if (index > -1) {
        temp.splice(index, 1)
      } else {
        temp.push(data)
      }
      this.$emit('update:selected', temp)
    }
  }
}
</script>

<style lang="scss">
.cpt-dropdown-list {
  display: inline-block;

  .dropdown-link {
    color: #409eff;
    cursor: pointer;
  }
}
</style>
