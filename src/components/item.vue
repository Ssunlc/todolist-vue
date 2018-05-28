<template>
    <div :class="['todo-item',todo.completed ? 'completed' : '']" >
        <input 
           type="checkbox"
           class="toggle"
           v-model="todo.completed"
        >
        <label>{{todo.content}}</label>
        <button class="destroy" @click="deleteTodo"></button>
    </div>
</template>

<script>
    export default{
        //父子组件间传递数据
        props:{
            //接收父组件传过来的todo，并判断是否为需要的类型
            todo:{
                type:Object,
                required:true
            }
        },
        methods: {
            deleteTodo(){
                //this.$emite出发del事件，并向监听的父组件返回数据：todo.id
                this.$emit('del',this.todo.id)
            }
        }
    }
</script>

<style lang="scss" scoped>
.todo-item{
    position: relative;
    background-color: #fff;
    font-size: 24px;
    border-bottom: 1px solid rgba(0,0,0,0.06);
    &:hover{
        .destroy::after{
            content: 'x'
        }
    }
    label{
            white-space: pre-line;
            word-break: break-all;
            padding: 15px 60px 15px 15px;
            margin-left: 45px;
            display: block;
            line-height: 1.2;
            transition: color 0.4s;
        }
        &.completed{
            label{
                color: #d9d9d9;
                text-decoration: line-through
            }
        }
    .toggle{
        text-align: center;
        width: 40px;
        height: 40px;
        line-height: 40px;
        position:absolute;
        top: 0;
        bottom: 0;
        appearance: none;
        margin: auto 0;
        outline: none;
        // border: none;
        padding-left: 5px;
        cursor: pointer;
        &:after{
            content: url('../assets/images/round.svg')
        }
        &:checked:after{
            content: url('../assets/images/done.svg')
        }
    }
}
 .destroy{
        position: absolute;
        top: 0;
        right: 10px;
        bottom: 0;
        width: 40px;
        height: 40px;
        margin: auto 0;
        font-size: 30px;
        color: #cc9a9a;
        margin-bottom: 11px;
        transition: color 0.2s ease-out;
        background-color: transparent;
        appearance: none;
        border-width: 0;
        cursor: pointer;
        outline: none;
    }
</style>
