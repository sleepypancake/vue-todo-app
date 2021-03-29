<template>
  <div class="shopping-list-container">
    <div class="header">
      <h1>{{header || 'Hello!'}}</h1>
      <button v-if="editing" @click="doEdit(false)" class="btn btn-cancel">
      Закрыть
      </button>
      <button v-else @click="doEdit(true)" class="btn btn-primary">Добавить штучку</button>
    </div>
    <div v-if="editing" class="add-item-form">
      <input 
      @keyup.enter="saveItem"
      type="text" v-model="newItem" placeholder="Добавь новую штуку">

      <p class="counter">{{characterCount}}/200</p>
      <button
        @click="saveItem" 
        :disabled="newItem.length === 0"
        class="btn btn-primary">
        Добавить штучку 
      </button>
    </div>

    <ul>
      <li 
        v-for="item in reversedItems" 
        :key="item"
        :class="{strikeout: item.done}"
        @click="toggleDone(item)">
      {{item.label}}
      </li>
    </ul>
    <p v-if="items.length === 0">Больше нет никаких штучек :(</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      editing: false,
      header: 'Список всяких штук',
      newItem: '',
      items: [
        {
          label: 'погладить пёпселя',
          done: false
        },
        {
          label: 'поспать',
          done: false
        },
        {
          label: 'покушать',
          done: false
        }
      ]
    }
  },
  components: {
    
  },
  methods: {
    saveItem() {
      this.items.push({
        label: this.newItem,
        done: false
      })
      this.newItem = ''
    },
    doEdit(editing){
      this.editing = editing
      this.newItem = ''
    },
    toggleDone(item){
      item.done = !item.done
    }
  },
  computed: {
    characterCount(){
      return this.newItem.length
    },

    reversedItems(){
      return [...this.items].reverse()
    }
  }
}
</script>

<style>
  body {
    margin: 0;
  }

  #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
      margin-top: 0;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background: #eee;
  }

  .shopping-list-container {
    background: #fff;
    padding: 40px 70px;
  }

  .add-item-form input {
    font-size: 14px;
    padding: 7px 10px;
    width: 300px;
    border: 1px solid #bbb;
    color: #2c3e50;
  }

  .btn {
    background: #4fc08d;
    border: 1px solid #4fc08d;
    border-radius: 10px;
    font-size: 14px;
    color: #2c3e50;
    font-weight: 600;
    padding: 7px 14px;
    max-height: 32px;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  li{
      text-align: left;
      font-size: 18px;
      margin-bottom: 7px;
  }

  p{
    text-align: left;
  }

  p.counter {
    margin: 0 10px;
  }

  .header {
    display: flex;
    align-items: center;
  }

  h1 {
    padding-right: 40px;
  }

  .btn-cancel {
    background: #cb6556;
    border: 1px solid #cb6556;
  }

  .btn:hover, .btn:focus, .btn:active{
    background: #fff;
    border: 1px solid #4fc08d;
    border-radius: 10px;
  }

  .btn-cancel:hover, .btn-cancel:focus, .btn-cancel:active{
    border: 1px solid #4fc08d;
  }

  button.btn:disabled {
    color: #bbb;
    background-color: #eee;
    border-color: #bbb;
  }

  li.strikeout{
    color: #bbb;
    text-decoration: line-through;
  }

  .add-item-form {
      display: flex;
      align-items: center;
      justify-content: space-between;
  }
</style>
