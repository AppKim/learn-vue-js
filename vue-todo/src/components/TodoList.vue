<template>
  <div>
      <ui>
          <li></li>
          <li></li>
          <li></li>
      </ui>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            todoItems: []
        }
    },
    created() {
        if (localStorage.length > 0) {
            for(var i=0; i < localStorage.length; i++){
                this.todoItems.push(localStorage.key(i))
            }
        }
    }
}
</script>

<style>

</style>