<template>
    <ul class="todo-main">
        <list-item v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo" />
    </ul>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
    name: 'MyList',
    components: { ListItem },
    props: ['todos', 'checkTodo'],
};
</script>

<style scoped>
/*main*/
.todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
}

.todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
}
</style>
