<template>
  <div class="inputBox shadow">
    <input type="text" placeholder="일정을 입력하세요." v-model="newTodoItem" v-on:keypress.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo" >
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
        <h3 slot="header">경고</h3>
         <span slot="footer" @click="showModal = false">일정을 입력하세요.
           <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
         </span>
    </modal>
  </div>
</template>

<script>
// ** Modal 띄우기 
import Modal from './common/Modal.vue'

  export default {
    data() {
      return {
        newTodoItem: '',
        showModal: false // 모달 동작을 위한 플래그 값
      }
    },
    methods: {
      addTodo() {
        console.log('newTodoItem =>'+this.newTodoItem);
         if (this.newTodoItem !== "") {
            var value = this.newTodoItem.trim();
            // localStorage.setItem(value, value); -> 상위 컴포넌트에서 처리 
            this.$emit('addTodo', value);
            this.clearInput();
         } else {
            //=> 일정 텍스트 미입력 시 모달 동작 : this.showModal 를 true 가 되도록 
            this.showModal = !this.showModal;
         }
      },
      clearInput() {
        this.newTodoItem = "";
      }
    },
    components: {
      Modal: Modal // 모달 컴포넌트 등록
    }
  }
</script>

<style scoped>
  ::placeholder {
    color: dimgray;
    font-size: 0.9rem;
    text-align: center;
  }
   input:focus {
      outline: none;
   }
   .inputBox {
      background: white;
      height: 50px;
      line-height: 50px;
      border-radius: 5px;
   }
   .inputBox input {
      border-style: none;
      font-size: 0.9rem;
      text-align: center;
   }
   .addContainer {
      float: right;
      background: linear-gradient(to right, #f56ba4, #b097ff);
      display: block;
      width: 3rem;
      border-radius: 0 5px 5px 0;
   }
   .addBtn {
      color: white;
      vertical-align: middle;
   }
</style>