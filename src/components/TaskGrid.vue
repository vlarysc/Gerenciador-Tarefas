<template>
<div class="task-grid">
    <template v-if="tasks.length">
        <Task v-for="(task, i) in tasks" :key="task.name" @taskDeleted="$emit('taskDeleted', i)" @taskStateChanged="$emit('taskStateChanged', i)" :task="task">  </Task>
    </template>
    <p v-else class="no-task">Parece que alguém está com a vida em dia &#129496;</p>
</div>
  
</template>

<script>
import Task from './Task'

export default {
    components: { Task },
    
    props: {
        tasks: {type: Array, requerid: true }
    }

}
</script>

<style>
.task-grid {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

.task-grid .task {
    margin: 10px;
}

.no-task {
    font-size: 3rem;
    color: #AAA;
}

</style>