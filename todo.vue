<template>
<div class="container">
    <h2 class="text-center mt-5">My To Do App</h2>
    <div class="d-flex">
        <input type="text" class="form-control" placeholder="Enter task" v-model="task">
        <button @click="enterTask" class="btn btn-warning rounded-0">Submit</button>
    </div>
</div>
<table class="table table-bordered mt-5">
    <thead>
        <tr>
            <th scope="col">Number</th>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col">Edit</th>
            <th scope="col">Delete</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
            <th scope="row">{{task.number}}</th>
            <td>{{task.name}}</td>
            <td>{{task.status}}</td>
            <!--<td>
                <div>
                     <span><i class="bi bi-paperclip"></i></span>
                    <input type="image"></div>
            </td>-->
            <td>
                <div @click="editTask(index)">
                    <span><i class="bi bi-pen"></i></span>
                </div>
            </td>
            <td>
                <div @click="deleteTask(index)">
                    <span><i class="bi bi-trash"></i></span>
                </div>
            </td>
        </tr>

    </tbody>
</table>
</template>

<script>
/*import {
    warn
} from '@vue/runtime-core';*/
export default {
    data() {
        return {
            task: '',
            number: '1',
            editedTask: null,
            tasks: [{
                    name: 'Go to school',
                    status: 'todo',
                    number: '1'

                },
                {
                    name: 'prepare the diary',
                    status: 'in-progress',
                    number: '2'

                }

            ]
        }
    },
    methods: {
        enterTask() {
            if (this.task.length === 0) return;

            if (this.editedTask === null) {
                this.tasks.push({
                    name: this.task,
                    status: 'to-do',
                    number: this.number++

                });
            } else {
                this.tasks[this.editedTask].name = this.task;
                this.editedTask = null;
            }

            this.task = '';

        },
        deleteTask(index) {
            this.tasks.splice(index, 1)

        },
        editTask(index) {
            this.task = this.tasks[index].name;
            this.editedTask = index;
        }
    }

}
</script>

<style>

</style>
