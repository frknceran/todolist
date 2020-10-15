<template>
    <div class="list-item">
        <div class="list-item-text">
            <div>
                <h6
                    ref="title"
                    :style="{textDecoration: editingTodo.done ? 'line-through' : 'none'}"
                    :contenteditable="isEditing"
                    @keypress.enter.prevent="handleEditFinish"
                >
                    {{ editingTodo.todo }}
                </h6>
            </div>
            <div class="button">
                <button class="delete" @click="handleDelete">
                    <ion-icon name="trash-outline"></ion-icon>
                </button>
                <button class="edit" @click="handleEdit">
                    <ion-icon name="create-outline"></ion-icon>
                </button>
                <button class="done" @click="handleDone">
                    <ion-icon name="checkmark-outline"></ion-icon>
                </button>
            </div>
        </div>
    </div>    
</template>
<script src="https://unpkg.com/ionicons@5.2.3/dist/ionicons.js"></script>
<script>
export default {
    name: "List",

    data() {
        return {
            isEditing: false,
            editingTodo: {
                todo: "",
                done: false
            }
        }
    },

    props: {
        selected: {
            type: Object,
            required: true
        }
    },

    watch: {
        editingTodo(value) {
            this.$emit("handleEdit", this.editingTodo)
        }
    },

    methods: {
        handleDelete() {
            this.$emit("handleDelete", this.selected)
        },
        handleDone() {
            this.editingTodo.done = !this.editingTodo.done
            //this.selected.css("text-decoration", "line-through") 
        },
        handleEdit() {
            this.isEditing = !this.isEditing
            
            setTimeout(() => {
                this.$refs.title.focus()
            }, 10)
        },

        handleEditFinish(e) {
            this.$refs.title.blur()
            this.$emit("handleEdit", this.editingTodo)
        }
    },

    mounted() {
        this.editingTodo = {...this.selected}
    }
}
</script>
<style scoped>
    .list-item {
        width: 100%;
    }
    .list-item-text {
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 5px 0px; 
        font-size: 30px;
    }
    .text {
        width: 100%;
    }
    .button button {
        font-size: 30px;
        border: none; 
        margin: 5px 0px;
        background-color: #fff;  
        border-radius: 10px;
    }
    button:focus {
        outline: none;
    }
    .delete:hover {
        background-color: #d61111;
        color: #ffffff;
    }
    .edit:hover {
        background-color: #d9dc29;
        color: #ffffff;
    }
    .done:hover {
        background-color:#48da18;
        color: #ffffff;
    }
    .list-item-text h6 {
        margin: 5px  auto;
        width: 100%;
    }

</style>