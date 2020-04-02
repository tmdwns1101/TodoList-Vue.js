<template>
<div>
  <div class="input-box shadow">
      <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
      <span class="add-container" v-on:click="addTodo">
          <i class="addBtn fas fa-plus" aria-hidden="true"></i>
      </span>
  </div>

  <Modal v-show="showModal" @closeModal="handleCloseModal">
      <template slot="header">
         <h3>경고</h3>
      </template>
      <template slot="body">
          <p>할 일을 입력해주요!!</p>
      </template>
  </Modal>
</div>
</template>

<script>
import ModalVue from './commons/Modal.vue';

export default  {
    data () {
        return {
            newTodoItem: '',
            showModal: false
        }
    },
    components: {
        Modal: ModalVue
    },
    methods: {
        addTodo() {
            if(this.newTodoItem !== "") {
                const value = this.newTodoItem && this.newTodoItem.trim();
                //localStorage.setItem(value, value);
                this.$emit('addTodo', value);
                this.cleaerInput();
            }
            else {
                //alert("You must input your Todo!");
                this.showModal = true;
            }
            
        },

        cleaerInput() {
            this.newTodoItem = "";
        },

        handleCloseModal() {
            this.showModal = false;
        }
    }
}
</script>

<style scoped>
    input:focus {
        outline: none;
    }

    .input-box {
        background: #fff;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }

    .input-box input {
        border-style: none;
        font-size: 0.9rem;
    }

    .add-container {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }

    .addBtn {
        color: white;
        vertical-align: middle;
    }

    .modal-header h3{
        color: #42b983;
    }
</style>

