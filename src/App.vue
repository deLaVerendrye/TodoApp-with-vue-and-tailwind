<script>


  let id = 0

export default{

  data(){
    return{
      count: 0,
      newTask: '',
      showCompleted: false,
      tasks: []
    }
  },

  computed: {
    filterTasks(){
      return this.showCompleted  ? this.tasks : this.tasks.filter(e => !e.done)
    }
  },

  methods: {
    addTask(){
      this.newTask ? this.tasks.push({id: id++, text: this.newTask, done: false}) : this.tasks

      this.newTask = ''
    },

    removeTask(task){
      this.tasks = this.tasks.filter(e => e !== task)
    }
  }

}
</script>

<template>
    <div class="w-96 bg-slate-700 mx-auto rounded-md p-5 grid content-center font-Nova">


      <h1 class="text-white font-bold text-3xl m-3 text-center">myTODO App</h1>


      <input type="text" v-model="newTask" @keyup.enter="addTask" placeholder="New Task" class="outline-none rounded-sm my-1 px-1 text-sky-700 text-center bg-slate-300">
      <button @click="addTask" class="bg-sky-300 my-1 rounded-sm active:bg-sky-400 text-slate-700 outline-none ">add task</button>


      <button @click="showCompleted = !showCompleted" class="bg-sky-200 my-1 rounded-sm active:bg-sky-300 text-slate-700 outline-none">
        {{showCompleted ? 'hide completed': 'show completed'}}
      </button>

      <div class="h-52 overflow-y-scroll">
        <ul>
          <li v-for="task in filterTasks" :key="task.id" class="text-sky-300 text-xl m-3 flex justify-start">
            <span>
              <input type="checkbox" v-model="task.done" title="finish" class="appearance-none h-4 w-4 border-2 border-sky-300 rounded-sm checked:bg-green-600 checked:border-green-400 hover:cursor-pointer outline-none">
            </span>
            <span :class="{ done: task.done}" class="mx-2">{{task.text}}</span>
            <span class="ml-auto">
              <button @click="removeTask(task)" class="px-1 rounded-lg text-md bg-slate-500 hover:bg-red-300 text-slate-700 outline-none">remove</button>
            </span>
          </li>
        </ul>
      </div>
    </div>
</template>



<style>

.done{
  text-decoration: line-through;
  color: rgb(118, 226, 150);
}

/* width */
::-webkit-scrollbar {
  width: 5px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f100; 
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(121, 176, 212); 
  border-radius: 25px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555; 
}

</style>