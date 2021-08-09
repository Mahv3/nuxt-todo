<template>
    <div style="margin : 20px">
        <ul>
            <input placeholder="タスクを追加" @keyup.enter="addTodo" />

            <li v-for="(todo,index) in todos" :key="todo.index">
                <input type="checkbox" :checked="todo.done" @change="toggle(todo)" />
                <span :class="{ done: todo.done }">{{ todo.text }}</span>
                <button @click="deleteTodo(index)">delete</button>
            </li>
        </ul>
        <button @click="deleteDone">delete done</button>
    </div>
</template>

<script>
import { mapMutations } from "vuex";
export default {
    computed: {
        todos() {
            return this.$store.state.todos.list;
        }
    },
    methods: {
        addTodo(e) {
            if (e.target.value == "") {
                return alert("タスクを入力してください");
            }
            this.$store.commit("todos/add", e.target.value);
            e.target.value = "";
        },
        ...mapMutations({
            toggle: "todos/toggle"
        }),
        deleteTodo(index) {
            this.$store.commit("todos/delete", index);
        },
        deleteDone() {
            this.$store.commit("todos/deleteDone");
        }
    }
};
</script>

<style>
.done {
    text-decoration: line-through;
}
ul {
    list-style-type: none;
}
</style>
