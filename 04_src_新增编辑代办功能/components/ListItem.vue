<template>
    <li>
        <label>
            <!-- 也可以实现功能呢，但不推荐，因为违反数据单向传递的原则（props 不允许修改值） -->
            <!-- <input type="checkbox" v-model="todo.done" /> -->
            <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)" />
            <span v-show="!todo.isEdit">{{ todo.title }}</span>
            <input
                type="text"
                v-show="todo.isEdit"
                ref="inputTitle"
                :value="todo.title"
                @blur="handleBlur(todo, $event)"
            />
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
        <button class="btn btn-edit" v-show="!todo.isEdit" @click="handleEdit(todo)">编辑</button>
    </li>
</template>

<script>
export default {
    name: 'ListItem',
    // 声明接收 todo 对象
    props: ['todo'],
    methods: {
        // 勾选或取消勾选
        handleCheck(id) {
            // 通知 app 组件将对应的 todo 对象的 done 值取反
            // this.checkTodo(id);

            this.$bus.$emit('checkTodo', id);
        },
        // 删除
        handleDelete(id) {
            // 通知 app 组件删除对应的 todo 对象
            if (confirm('确定删除吗？')) {
                // this.deleteTodo(id);

                this.$bus.$emit('deleteTodo', id);
            }
        },
        // 点击编辑按钮事件
        handleEdit(todo) {
            // todo.isEdit = true;
            if (todo.hasOwnProperty('isEdit')) {
                todo.isEdit = true;
            } else {
                this.$set(todo, 'isEdit', true);
            }

            // 如果不使用定时器或 nextTick, 获取焦点将失败, 因为执行获取焦点代码时 vue 未更新 DOM
            // setTimeout(() => {
            //     this.$refs.inputTitle.focus();
            // });
            this.$nextTick(function () {
                this.$refs.inputTitle.focus();
            });
        },
        // 失去焦点回调, 修改todo内容
        handleBlur(todo, e) {
            todo.isEdit = false;
            if (e.target.value.trim() === '') {
                this.$bus.$emit('updataTodo', todo.id, e.target.value);
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
