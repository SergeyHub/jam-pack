<template>

    <div
            @dblclick="$emit('toggle-reminder', jam.id)"
            :class="[jam.reminder ? 'reminder' : '', 'jam']"
    >
        <h4>Jam Name =
            {{ jam.text }}
            <i @click="$emit('delete-jam', jam.id)" class="fas fa-times"></i>
        </h4>
        <p>Amount = {{ jam.amount }} g</p>
    </div>


</template>


<script>
    export default {
        name: 'Jam',
        props: {
            jam: Object,
        },
    }
</script>

<style scope>
    .fas {
        color: red;
    }

    .jam {
        background: #f1f1f1;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
        width: 310px;
    }

    .jam.reminder {
        border-left: 5px solid green;
    }

    .jam h4 {
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-family: 'Poppins', sans-serif;
        font-size: 13px;
        font-weight: 400;
        /*color: lightyellow;*/
    }

    .jam p {
        font-size: 13px;
        /*color: lightyellow;*/
    }


</style>
