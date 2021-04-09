<template>
    <header>
        <h3>{{ title }}</h3>
        <Button
                v-show="homePage"
                @btn-click="$emit('toggle-add-task')"
                :text="showAddTask ? 'Close' : 'Add Container'"
                :color="showAddTask ? 'red' : 'green'"
        />
        <Button
                v-show="homePage"
                @btn-click="$emit('toggle-add-jam')"
                :text="showAddJam ? 'Close' : 'Add Jam'"
                :color="showAddJam ? 'red' : 'green'"
        />
        <Button text="Pack Jam" color="blue"/>
        <Button text="Show Pack Jam" color="blue"/>
    </header>
</template>

<script>
    import Button from './Button'

    export default {
        name: 'Header',
        props: {
            title: String,
            showAddTask: Boolean,
            showAddJam: Boolean,
        },
        components: {
            Button,
        },
        computed: {
            homePage() {
                if (this.$route.path === '/') {
                    return true
                } else {
                    return false
                }
            },
        },
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 3px;
        padding-bottom: 20px;

        border-bottom: solid 1px black;

    }
</style>
