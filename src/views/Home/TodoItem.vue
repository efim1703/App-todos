<template>
    <div class="todo-item">
        <h3 class="todo-name">{{ todo.name }}</h3>
        <div class="todo-list">
            <div :class="[ index > 4 ? 'd-none' : '' ,'todo-list-item' ]" v-for="(todoListItem, index) in todo.todoList" :key="todoListItem.id">
                <input type="checkbox" v-model="todoListItem.completed">
                <span :class="[ todoListItem.completed ? 'line-trought' : '' ]">{{ ++index }}.   {{todoListItem.name}}</span>
                <span class="and-more" v-show="index == 5">И ещё несколько.....</span>
            </div>
            
        </div>
        <div class="todo-actions">
            <router-link to="/create">
                <c-btn 
                    class="change-btn"
                    @click="$emit('get-todo', todo)"
                >
                    Редактировать
                </c-btn>
            </router-link>
        </div>
    </div>
</template>

<script>
import CBtn from '@/components/CBtn.vue'
export default {
    components: { CBtn },
    name: 'TodoItem',
    props: {
        todo: Object,
    },
    methods: {
    }
}
</script>

<style scoped>
    .todo-item {
        display: none;
    }
    .todo-item{
        display: flex;
        flex-direction: column;
        width: calc(100%/2 - 62px);
        padding: 16px;
        min-height: 200px;
        max-height: 200px;
        box-shadow: 0px 8px 16px rgba(0 0 0 /10%);
        border-radius: 8px;
    }
    .todo-name {
        text-align: center;
        margin-bottom: 12px;
    }
    .todo-list {
        margin-bottom: 12px;
    }
    .todo-list input{
        margin-right: 8px;
    }
    .todo-actions {
        margin-top: auto;
        width: 100%;
    }
    .todo-actions a{
        text-decoration: none;
        display: flex;
        justify-content: end;
        margin-left: auto;
        width: 100%;
    }
    .change-btn {
        margin-left: auto;
    }
    .d-none {
        display: none;
    }
    .line-trought {
        text-decoration: line-through;
    }
    .and-more {
        margin-top: 16px;
        display: block;
    }
</style>