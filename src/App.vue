<template>
    <main>
        <!-- Heading -->
        <header>
            <img src="@/assets/pinia-logo.svg" alt="Pinia Logo">
            <h1>Pinia Tasks</h1>
        </header>

        <!-- New Task Form -->
        <div class="new-task-form">
            <TaskForm></TaskForm>
        </div>

        <!-- Filter -->
        <nav class="filter">
            <button @click="(filter = 'all')">All tasks</button>
            <button @click="(filter = 'favs')">Fav tasks</button>
        </nav>

        <!-- Task List -->
        <div class="task-list" v-if="filter === 'all'">
            <p>Your have {{ taskStore.totalCount }} tasks left to do</p>
            <div v-for="task in taskStore.tasks">
                <TaskDetails :task="task"></TaskDetails>
            </div>
        </div>
        <div class="task-list" v-else>
            <p>Your have {{ taskStore.favsCount }} favs left to do</p>
            <div v-for="task in taskStore.favs">
                <TaskDetails :task="task"></TaskDetails>
            </div>
        </div>
    </main>
</template>

<script>
    import { ref } from 'vue';
    import { useTaskStore } from './stores/TaskStore.js';
    import TaskDetails from './components/TaskDetails.vue';
    import TaskForm from './components/TaskForm.vue';
    
    export default {
        name: 'app',
        components: { TaskDetails, TaskForm },  
        setup() {
            const taskStore = useTaskStore();
            
            const filter = ref('all');

            return {
                taskStore,
                filter
            }
        }
    }
</script>

<style scoped></style>