<template>
    <li v-bind:class="taskClassName">
        <button className="delete" @click="deleteThisTask">
            x
        </button>
        <input
            type="checkbox"
            readOnly 
            v-bind:checked="!!this.task.checked"
            @click="toggleChecked"
        />   

            <span>{{ this.task.text }}</span>
            </li>
</template>

<script>
import { Tasks } from "../api/tasks.js";

export default {
    props: ["task"],
    data() {
        return {};
    },
    computed: {
        taskClassName: function() {
            return this.task.checked ? "checked" : "";
        }
    },
    methods: {
        toggleChecked(){
            // Set the checked property to the opposite of its current velue
            Tasks.update(this.task._id, {
                $set: {checked: !this.task.checked }
            });
        },
        deleteThisTask() {
            Tasks.remove(this.task._id);
        }
    }
};
</script>