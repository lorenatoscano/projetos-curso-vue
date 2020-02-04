<template>
    <div class="task-list">
        <template v-if="tasks.length">
            <task v-for="(item, i) in tasks" :key="item.name" 
            @taskDeleted="$emit('taskDeleted', $event)"
            @taskStateChanged="$emit('taskStateChanged', i)"
            :task="item"></task>
        </template>
        <p class="no-task" v-else>Sua vida está em dia :)</p> 
    </div>
</template>

<script>
import Task from './Task.vue'
export default {
    components: { Task },
    props: {
        tasks: {
            type: Array,
            required: true
        }
    }
}
</script>

<style>
    .task-list {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
    .task-list .task {
        margin: 10px;
    }
    .task-list .no-task {
        color: #AAA;
        font-size: 1.7rem;
    }
</style>