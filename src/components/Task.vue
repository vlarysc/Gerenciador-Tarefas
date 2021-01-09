<template>
<div 
@click="$emit('taskStateChanged', task)"
class="task" :class="stateClass">
    <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
   <p> {{ task.name }} </p>
</div>
  
</template>

<script>

export default {
    props: {
      task:  { type: Object, required: true }
    
    },
    computed: {
        stateClass() {
            return {
            pending: this.task.pending,
            done: !this.task.pending
        }
        }
    }
}
</script>

<style>
.task {
    position: relative;
    box-sizing: border-box;
    width: 300px;
    height: 100px;
    padding: 10px;
    border-radius: 50px;
    font-size: 2rem;
    font-weight: 600;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
}

.pending {
    border-left: 12px solid rgb(240, 25, 25);
    background-color: rgb(243, 86, 86);
}

.done {
    color: white;
    border-left: 12px solid green;
    background-color: greenyellow;
    text-decoration: line-through;
}

.pending .close {
    background-color: rgb(233, 30, 30);
}
.done .close {
    background-color:  rgb(50, 207, 50);
}

.close {
    position: absolute;
    right: 10px;
    top: 10px;   
    width: 20px;
    height: 20px;
    border-radius: 10px;
    font-size: 0.9rem;
    font-weight: 600;
    display: flex;
    justify-content: center;
    margin: 30px 0px;
}


</style>