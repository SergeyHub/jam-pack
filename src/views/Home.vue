<template>
    <AddTask v-show="showAddTask" @add-task="addTask"/>
    <AddJam v-show="showAddJam" @add-jam="addJam"/>
    <div class="container">
        <div class="item">
            <Tasks
                    @toggle-reminder="toggleReminder"
                    @delete-task="deleteTask"
                    :tasks="tasks"
            />
        </div>
        <br>
        <div class="item">
            <Jams
                    @toggle-reminder="toggleReminderJam"
                    @delete-jam="deleteJam"
                    :jams="jams"
            />
    </div>
    </div>
</template>

<script>
    import Tasks from '../components/Tasks'
    import Jams from '../components/Jams'
    import AddTask from '../components/AddTask'
    import AddJam from '../components/AddJam'

    export default {
        name: 'Home',
        props: {
            showAddTask: Boolean,
            showAddJam: Boolean,
        },
        components: {
            Tasks,
            Jams,
            AddTask,
            AddJam,
        },
        data() {
            return {
                tasks: [],
                jams: [],
            }

        },
        methods: {
            async addTask(task) {
                const res = await fetch('api/tasks', {
                    method: 'POST',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(task),
                });

                const data = await res.json();

                this.tasks = [...this.tasks, data]
            },
            // ..........................................
            async addJam(jam) {
                const res = await fetch('api/jams', {
                    method: 'POST',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(jam),
                });

                const data = await res.json();

                this.jams = [...this.jams, data]
            },
            // ..........................................
            async deleteTask(id) {
                if (confirm('Are you sure?')) {
                    const res = await fetch(`api/tasks/${id}`, {
                        method: 'DELETE',
                    });

                    res.status === 200
                        ? (this.tasks = this.tasks.filter((task) => task.id !== id))
                        : alert('Error deleting container')
                }
            },
            // ..........................................
            async deleteJam(id) {
                if (confirm('Are you sure?')) {
                    const res = await fetch(`api/jams/${id}`, {
                        method: 'DELETE',
                    });

                    res.status === 200
                        ? (this.jams = this.jams.filter((jam) => jam.id !== id))
                        : alert('Error deleting jam')
                }
            },
            // ..........................................
            async toggleReminder(id) {
                const taskToToggle = await this.fetchTask(id);
                const updTask = {...taskToToggle, reminder: !taskToToggle.reminder};

                const res = await fetch(`api/tasks/${id}`, {
                    method: 'PUT',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(updTask),
                });

                const data = await res.json();

                this.tasks = this.tasks.map((task) =>
                    task.id === id ? {...task, reminder: data.reminder} : task
                )
            },
            // ..............................................
            async toggleReminderJam(id) {
                const jamToToggle = await this.fetchTask(id);
                const updJam = {...jamToToggle, reminder: !jamToToggle.reminder};

                const res = await fetch(`api/jams/${id}`, {
                    method: 'PUT',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(updJam),
                });

                const data = await res.json();

                this.jams = this.jams.map((jam) =>
                    jam.id === id ? {...jam, reminder: data.reminder} : jam
                )
            },
            // ..............................................
            async fetchTasks() {
                const res = await fetch('api/tasks');

                const data = await res.json();

                return data
            },
            // ..............................................
            async fetchJams() {
                const res = await fetch('api/jams');

                const data_jam = await res.json();

                return data_jam
            },
            // ..............................................
        }, //end methods
        async created() {
            this.tasks = await this.fetchTasks();
            this.jams = await this.fetchJams()
        },
    }
</script>

<style>
    .container{
        display: inline-flex;
    }
</style>
