<template>
    <div class="create">
        <div class="todo-item-created">
            <h2 @click="showInputNameTodo = true" v-show="!showInputNameTodo">{{ todoClon.name }}   &#9998;</h2>
            <input 
                v-show="showInputNameTodo" 
                @keyup.enter="changeNameTodo($event)" 
                type="text" class="input-new-todo" 
                v-model="inputNameTodo"
            >
            <div 
                class="todo-list-item" 
                v-for="(todoListItem, index) in todoClon.todoList"
                :key="todoListItem.id"
            >
                <input type="checkbox" v-model="todoListItem.completed">
                <span 
                    :class="[ todoListItem.completed ? 'line-trought' : '' ]"
                >
                    {{ ++index }}.   {{todoListItem.name}}
                </span>
                <button @click="deleteTodoListItem(todoListItem.id)">
                    &#10006;
                </button>
            </div>
            <input 
                v-show="showInputNewTodoListItem" 
                @keyup.enter="addTodoListItem($event)" 
                type="text" class="input-new-todo" 
                v-model="inputNewTodoListItem"
            >
            <c-btn class="add-btn" color="green" @click="showInput()">+</c-btn>
            <div class="todo-actions">
                <c-btn class="change-btn" @click="openSaveModal()" >Cохранить изминения</c-btn>
                <c-btn color="rgb(184, 25, 25)"  @click="openDeleteModal()" >Удалить</c-btn>
            </div>
        </div>
        <div class="modal" :style="{ display: showIsModalSave ? 'flex' : 'none' }">
            <h3>Сохранить изменения?</h3>
            <c-btn @click="saveTodo()">Сохранить</c-btn>
            <c-btn color="red" @click="cancelChanged()">Отменить изменения</c-btn>
        </div>
        <div class="modal" :style="{ display: showIsModalDelete ? 'flex' : 'none' }">
            <h3>Точно удалить?</h3>
            <c-btn color="red" @click="deleteTodo()">Удалить</c-btn>
            <c-btn @click="exitDeleteModal()">Отменить удаление</c-btn>
        </div>
    </div>
</template>

<script>
import CBtn from '@/components/CBtn.vue'

export default {
    name: 'CreateView',
    components: {
        CBtn
    },
    props: {
        activeTodo: {
            type: Object
        }
    },
    mounted() {
        this.$nextTick(function () {
            this.todoClon = this.activeTodo
            this.inputNameTodo = this.todoClon.name
        })
    },
    data() {
        return {
            todoClon: {},
            showInputNewTodoListItem: false,
            inputNewTodoListItem: '',
            inputNameTodo: '',
            showIsModalSave: false,
            showIsModalDelete: false,
            showInputNameTodo: false
        }
    },
    methods: {
        deleteTodoListItem(id) {
            this.todoClon.todoList = this.todoClon.todoList.filter(el => el.id != id)
        },
        addTodoListItem(event) {
            let todoListItem = {
                id: Date.now(),
                name: event.target.value,
                completed: false
            }
            this.todoClon.todoList.push(todoListItem);
            this.showInputNewTodoListItem = false
            this.inputNewTodoListItem = ''
        },
        changeNameTodo(event) {
            this.todoClon.name = event.target.value
            this.showInputNameTodo = false
        },
        showInput() {
            this.showInputNewTodoListItem = true
            this.inputNewTodoListItem = ''
        },
        openSaveModal() {
            this.showIsModalSave = true
        },
        openDeleteModal() {
            this.showIsModalDelete = true
        },
        saveTodo() {
            this.$emit('save-todo', this.todoClon )
            this.showIsModalSave = false
        },
        cancelChanged() {
            this.todoClon = this.activeTodo
            this.showIsModalSave = false
        },
        deleteTodo() {
            this.$emit('delete-todo', this.todoClon )
            this.showIsModalDelete = false
            this.todoClon = {}
        },
        exitDeleteModal() {
            this.showIsModalDelete = false
        }
    }
}
</script>

<style scoped>
    h2 {
        width: 100%;
        margin-bottom: 12px;
    }
    .todo-item-created {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 400px;
        margin: 36px auto;
        padding: 24px;
        text-align: center;
        min-width: 400px;
        max-width: 400px;
        box-shadow: 0px 8px 16px rgba(0 0 0 /10%);
        border-radius: 8px;
    }
    .todo-list-item {
        display: flex;
        width: 100%;
        justify-content: space-between;
    }
    .todo-actions {
        display: flex;
        justify-content: end;
        width: 100%;
        margin-top: auto;
    }
    .input-new-todo {
        padding: 4px 8px;
        text-decoration: none;
        width: 80%;
        margin-bottom: 12px;
    }
    .change-btn {
        margin-right: 4px;
        margin-left: auto;
    }
    .add-btn {
        width: fit-content;
        margin: 12px 0;
        padding: 4px 6px;
    }
    .line-trought {
        text-decoration: line-through;
    }
    .modal {
        position: absolute;
        bottom: 50%;
        left: 50%;
        transform: translate(-50%, 50%);
        background-color: rgb(241, 227, 227);
        flex-direction: column;
        align-items: center;
        gap: 20px;
        width: 300px;
        padding: 24px;
    }
</style>