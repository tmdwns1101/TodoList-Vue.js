<template>
  <div class="clearAllContainer shadow" >
      <span class="clearAll" v-on:click="clearTodo" >Clear All</span>
  </div>
</template>

<script>
export default {
    methods: {
        clearTodo() {
          
           this.$emit('clearTodo');
        }
    }
}
</script>

<style scoped>
    .clearAllContainer {
        width: 8.5rem;
        height: 50px;
        line-height: 50px;
        background: white;
        border-radius: 5px;
        margin: 0 auto;
    }

    .clearAll {
        color: #e20303;
        display: block;
    }
</style>