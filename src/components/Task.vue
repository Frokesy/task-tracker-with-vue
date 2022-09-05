<template>
    <div @dblclick="$emit('toggle-task', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
        <span>
        {{ task.text }}
        <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </span>
    <p>
        {{ task.day }}
    </p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object,
    },
}
</script>

<style>
.task {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 10px 15px;
    background-color: #eee;
    border-bottom: 1px solid #ccc;
    margin-bottom: 10px;
}
.task span {
    font-size: 1.2rem;
    font-weight: bold;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.task i {
    font-size: 1rem;
    color: red;
    cursor: pointer;
}
.task p {
    font-size: 0.8rem;
    color: #999;
}
 .reminder {
    border-left: 3px solid green;
}
</style>