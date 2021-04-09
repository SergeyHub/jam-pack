<template>
    <div
            @dblclick="$emit('toggle-reminder', task.id)"
            :class="[task.reminder ? 'reminder' : '', 'task']"
    >
        <h4>Container Volume = {{ task.text }} g
            <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
        </h4>
        <p>Amount = {{ task.amount }}</p>
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

<style scope>
    .fas {
        color: red;
    }

    .task {
        background: #f9f9f9;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
        width: 310px;
    }

    .task.reminder {
        border-left: 5px solid green;
    }

    .task h4 {
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-family: 'Poppins', sans-serif;
        font-size: 13px;
        font-weight: 400;
    }

        .task p{
            font-size: 13px;
        }

</style>
