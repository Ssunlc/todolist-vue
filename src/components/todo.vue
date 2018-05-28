<template>
    <section class="real-app">
        <input 
           type="text"
           class="add-input"
           autofocus="autofocus"
           placeholder="准备做什么"
           @keyup.enter="addTodo"
        >
        <item :todo="todo" v-for="todo in filteredTodos" :key=todo.id @del="deleteTodo1"></item>
        <tabs 
            :filter="filter"
            :todos="todos"
            @toggle="toggleFilter"
            @clearAllCompleted="clearAllCompleted"
        ></tabs>
    </section>
</template>
<script>
    import Item from './item.vue';
    import Tabs from './tabs.vue';
    let id=0;
    export default {
        data(){
            return {
                todos:[],
                filter:'all',
            }
        },
        methods: {
            addTodo(e){
                this.todos.unshift({
                    id:id++,
                    content:e.target.value.trim(),
                    completed:false,
                }),
                e.target.value=''
            },
            deleteTodo1(id){
               this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
            },
            toggleFilter(state){
               this.filter = state;
            },
            clearAllCompleted(){
               // 给todos赋一个新的值（即todo.completed为false的值）
                this.todos = this.todos.filter(todo => todo.completed === false)
            }
        },
        computed:{
            //计算被tabs过滤后的todos，以便用于过滤后再列表渲染
            filteredTodos(){
                //点击all时，fillter不用过滤，使用最开始的todos就可以了
                if(this.filter ==='all'){
                    return this.todos;
                }
                //点击completed时，将completed赋值给变量completed
                const completed = this.filter === 'completed';
                // 将todos数组中，completed为true的值过滤出来，并返回一个新数组
                return this.todos.filter(todo => completed === todo.completed);
            }
        },
        components:{
            Item,
            Tabs
        }
    }
</script>

<style lang="scss" scoped>
 .real-app{
     width: 600px;
     margin:0 auto;
     box-shadow: 0 0 5px #666;
 }
 .add-input{
     position: relative;
     box-sizing: border-box;
     width: 100%;
     margin: 0;
     font-size: 24px;
     outline: none;
     padding: 16px 16px 16px 36px;
     border:none;
     box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);

 }
</style>

