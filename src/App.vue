<template>
    <div class="container">
        <div class="header">
            <Header
                    @toggle-add-task="toggleAddTask"
                    @toggle-add-jam="toggleAddJam"
                    title="Jam Packing App"
                    :showAddTask="showAddTask"
                    :showAddJam="showAddJam"

            />
        </div>
        <div class="inner">
            <router-view :showAddTask="showAddTask" :showAddJam="showAddJam"></router-view>
        </div>
    </div>
        <div class="total">Total Containers Volume= </div>
        <div class="total-jam">Total Jams Volume= </div>
        <Footer/>
</template>

<script>
    import Header from './components/Header'
    import Footer from './components/Footer'

    export default {
        name: 'App',
        components: {
            Header,
            Footer,
        },
        data() {
            return {
                showAddTask: false,
                showAddJam: false,
            }
        },
        methods: {
            toggleAddTask() {
                this.showAddTask = !this.showAddTask
            },
            toggleAddJam() {
                this.showAddJam = !this.showAddJam
            },
        },
    }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Poppins', sans-serif;
}

.container {
    max-width: 1100px;
    margin: 7px auto;
    overflow: auto;
    min-height: 300px;
    /*border-bottom: 1px solid steelblue;*/
    padding: 30px;
    border-radius: 0;
    /*background-color: red; /*lavender;*/
    display: flex;
    flex-wrap: wrap;
}

.container header{
    display: inline-flex;
    /*background-color: lemonchiffon;*/
}

.container header title{
    color: red;
}

.btn {
    display: inline-block;
    background: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    text-decoration: none;
    font-size: 15px;
    font-family: inherit;
}

.btn:focus {
    outline: none;
}

.btn:active {
    transform: scale(0.98);
}

.btn-block {
    display: block;
    width: 100%;
    }
</style>
