<!-- 
    2020-03-29 이슈 사항
    edit 버튼 누를 시 할 일 아이템을 수정 할 수 있도록 기능 추가
    // 2020-03-30 해결

    
-->
<template>
  <section>
      <transition-group name="list" tag="ul">
        <li class="shadow"  v-for="(todoItem,index) in propsdata" :key="index">
           
            <template v-if="editMode === true && index === editTodoIdx">
                <input type="text"  v-model="editedTodo" autofocus>
                <input type="button" class="btn confirmBtn" value="변경" @click="editConfirm(todoItem,index)">
            </template>
            <template v-else>
                <i class="checkBtn fas fa-check" aria-hidden="true" @click="toggleTodo(index)"></i>
                <p class="content" :class="{done: todoItem.done}">{{todoItem.todo}}</p>
                <span  class="btn editBtn" type="button" @click="editTodo(todoItem,index)">
                    <i class="fas fa-edit" aria-hidden="true"></i>
                </span>
                <span class="btn removeBtn" type="button" @click="removeTodo(todoItem, index)">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>

            </template>
            
        </li>
      </transition-group>
      
  </section>
</template>

<script>
export default {    
    props: ['propsdata'],
    
   
    data() {
        return {
            editedTodo: '',
            editMode: false,
            editTodoIdx: -1
        }
    },
    computed: {
        todoTitle(todoItem) {
            if(todoItem.done === true){

            }
        }
    },

    methods: {
        removeTodo(todoItem, index) {
            this.$emit('removeTodo',todoItem, index);
        },

        editTodo(todoItem, index) {
            this.editMode = true;
            this.editedTodo = todoItem.todo;
            this.editTodoIdx = index;
        },

        editConfirm(todoItem, index) {
           
            localStorage.removeItem(todoItem.todo);
            const editedTodoItem = {...todoItem, 'todo': this.editedTodo};
            console.log(editedTodoItem);
            this.$emit('editTodo', editedTodoItem, index);
            this.editMode = false;
            this.editedTodo = '';
            this.editTodoIdx = -1;

        },

        toggleTodo(index) {
            this.$emit('toggleTodo',index);
        }
    }
}
</script>



<style scoped>
    ul {
        list-style-type: none;
        padding-left: 0;
        margin-top: 0;
        text-align: left;
    }

    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
        align-items: center;
    }

    li .content {
        flex: 1;
    }
    li .done {
        text-decoration: line-through;
        opacity: 0.7;
    }
    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 10px;
    }


    .btn {
        margin-left: 5px;
    }

    .editBtn {
        color: #12b886;
    }
    .removeBtn {
       
        color: #de4343;
    }
    .confirmBtn {
        border: none;
        background: none;
        font-family: 'Do Hyeon', sans-serif;
        font-size: 1rem;
        font-weight: 300;
        color: #12b886;
    }
    .list-enter-active, .list-leave-active {
        transition: all 1s;
    }

    .list-enter, .list-leave-to {
        opacity: 0;
        transform: translateY(30px);
    }

</style>