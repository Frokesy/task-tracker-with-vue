<template>
  <div class="header">
    <h2>{{ title }}</h2>
    <Button @btn-click="$emit('show-new-task')" :text="showNewTask ? 'Close' : 'Add Task'" :color="showNewTask ? 'red' : 'green'" />
  </div>
</template>

<script>
import Button from './Button.vue';
export default {
    name: "Header",
    props: {
            title: String,
            showNewTask: Boolean
    },
    components: { Button }
}
</script>

<style>
    .header {
        font-size: 13px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 40px;
    }
</style>