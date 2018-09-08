<template>
    <div>
        <div>
            <span class="input">
                <input type="text" v-model="todo" placeholder="Add Todo" v-on:keyup.enter="addTodo"/>
                <span></span>	
            </span>
            <button class="button" style="background-color:#42b883" v-on:click="addTodo">Add</button>
            <button class="button" style="background-color:#36495d" v-on:click="deleteAll">Delete All</button>
        </div>
        <ul>
            <li class="list" v-for="(todo,index) in todoList" :key='index'>
                <span v-if="editIndex !== index">{{todo}}</span>
                <input v-else type="text" v-model="editTodoValue" v-on:keyup.enter="saveTodo(index)"/>
                <span v-if="editIndex !== index">
                    <button class="button" style="background-color:#42b883" v-on:click="editTodo(index)">Edit</button>
                    <button class="button" style="background-color:#36495d" v-on:click="removeTodo(index)">Delete</button>
                </span>
                <span v-else>
                    <button class="button" style="background-color:#36495d; margin-top: 10px" v-on:click="saveTodo(index)">Save</button>
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  name: 'Todo',
  data () {
    return {
      todoList: [],
      todo: '',
      editTodoValue: '',
      editIndex: null
    }
  },
    // define methods under the `methods` object
    methods: {
        addTodo: function (event) {
            if (this.todo !== '') {
                this.todoList.push(this.todo)
                this.todo = ''
            } else {
                alert('Please fill the input field')
                }
        },
        removeTodo: function (index) {
            this.todoList.splice(index, 1)
        },
        editTodo: function (index) {
            this.editIndex = index
            this.editTodoValue = this.todoList[index]
        },
        saveTodo: function (index) {
            this.todoList[index] = this.editTodoValue
            this.editTodoValue = ''
            this.editIndex = null
        },
        deleteAll: function () {
            this.todoList = []
            this.todo = ''
        }
    }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
    font-style: italic;
    font-size: 1.2em;
    font-style: italic; 
}
h1, h2 {
  font-weight: normal
}
ul {
  list-style-type: none;
  padding: 0
}
.button {
	-moz-border-radius:28px;
	-webkit-border-radius:28px;
	border-radius:28px;
	border:1px solid #18ab29;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:17px;
	padding:16px 31px;
	text-decoration:none;
	text-shadow:0px 1px 0px #2f6627;
}
.button:active {
	position:relative;
	top:1px;
}
input[type=text] {
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: none;
    background-color: #42b883;
    color: #fff;
    border-radius: 28px;
    border-color: #fff;
    padding:10px 21px;
}
input:focus, button:focus{
    outline: none;
}
input::placeholder { 
    color: #fff
}
ul {
    width: 700px;
    margin: 0 auto;
}
li {
    margin: 20px;
}
.list {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
</style>
