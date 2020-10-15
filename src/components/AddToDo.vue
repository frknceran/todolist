<template>
    <div id="add">
        <h1>My to-Dos</h1>
        <div class="adding">
            <input 
                type="text" 
                name="todo" 
                placeholder="Create a new to-do" 
                v-model="newTodo.todo"
                @keypress.enter="handleAdd"
            />
            <button @click="handleAdd">Add to List</button>
        </div>
        <List 
            v-for="(item, index) in dolist" 
            :key="index"
            :selected="item"
            @handleDelete="handleDelete"
            @handleDone="handleDone"
            @handleEdit="handleEdit"
        />
    </div>   
</template>
<script>
import List from "./List.vue"

export default {
    name: "AddToDo",

    components: {
        List
    },

    data() {
        return {
            newTodo: {
                todo: "",
                done: false
            },
            dolist: [],    
        }
    },

    methods: {
        handleAdd() {
            if(this.newTodo.todo) {
                this.dolist.push(this.newTodo)
                this.newTodo = {
                    todo: "",
                    done: false
                }
            }
        },

        handleDelete(selected) { 
            const index = this.dolist.findIndex(element => element.todo === selected.todo ) 
            this.dolist.splice(index,1)
            console.log(index)
        },

        handleEdit(selected) {
            const index = this.dolist.findIndex(element => element.todo === selected.todo) 
            this.dolist[index] = {...selected}
        },

        handleDone(selected) {
            const index = this.dolist.findIndex(element => element.todo === selected.todo)
            if(this.dolist[index].done === false) {
                this.dolist[index].done = true
            } else {
                this.dolist[index].done = false
            }
        },
    }
}

</script>

<style scoped>
    #add {
    }
    .adding {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }
    input {
        width:80%;
        font-size:25px;
    }
    input:focus {
        outline: none;
        box-shadow: 0 0 5px #2c23af;
    }
    button {
        border: none;
        background-color: #fff;
        border-radius: 10px;
    }
    button:hover {
        background-color: #0c7d10;
    }
</style>