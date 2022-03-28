<template>
    <li>
        <label>
            <!-- <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" /> -->
            <!-- 也可以实现功能呢，但不推荐，因为违反数据单向传递的原则（props 不允许修改值） -->
            <input type="checkbox" v-model="todo.done" />
            <span>{{ todo.title }}</span>
        </label>
        <button class="btn btn-danger" style="display: none">删除</button>
    </li>
</template>

<script>
export default {
    name: 'ListItem',
    // 声明接收 todo 对象
    props: ['todo'],
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
</style>
