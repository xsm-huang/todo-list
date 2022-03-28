<template>
    <li>
        <label>
            <!-- 也可以实现功能呢，但不推荐，因为违反数据单向传递的原则（props 不允许修改值） -->
            <!-- <input type="checkbox" v-model="todo.done" /> -->
            <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
            <span>{{ todo.title }}</span>
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    </li>
</template>

<script>
export default {
    name: 'ListItem',
    // 声明接收 todo 对象
    props: ['todo', 'checkTodo', 'deleteTodo'],
    methods: {
        // 勾选或取消勾选
        handleCheck(id) {
            // 通知 app 组件将对应的 todo 对象的 done 值取反
            this.checkTodo(id);
        },
        // 删除
        handleDelete(id) {
            // 通知 app 组件删除对应的 todo 对象
            if (confirm('确定删除吗？')) {
                this.deleteTodo(id);
                console.log(id);
            }
        },
    },
};
</script>

<style scoped>
/*item*/
li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
}

li label {
    float: left;
    cursor: pointer;
}

li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
}

li button {
    float: right;
    display: none;
    margin-top: 3px;
}

li:before {
    content: initial;
}

li:last-child {
    border-bottom: none;
}

li:hover {
    background-color: #ddd;
}
li:hover button {
    display: block;
}
</style>
