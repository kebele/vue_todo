<template>
  <div class="home">

          <v-text-field
          v-model="newTaskTitle"
          @click:append="addTask"
          @keyup.enter="addTask"
          class="pa-3"
            outlined
            label="add task"
            append-icon="mdi-pencil-plus"
            hide-details
            clearable
          ></v-text-field>

    <v-list flat class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'green lighten-1': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <!-- <v-checkbox :input-value="active" color="primary"></v-checkbox> -->
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn @click.stop="deleteTask(task.id)" icon>
                <v-icon color="red lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>

</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      newTaskTitle : "",
      tasks: [
        // {
        //   id: 1,
        //   title: 'uyan',
        //   done: false,
        // },
        // {
        //   id: 2,
        //   title: 'yüzünü yıka',
        //   done: false,
        // },
        // {
        //   id: 3,
        //   title: 'giyin',
        //   done: false,
        // },
      ],
    };
  },
  methods: {
    doneTask(id) {
      // console.log('id : ', id)
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    addTask(){
      // console.log("add task");
      let newTask = {
        id : Date.now(), //unique id için
        title : this.newTaskTitle,
        done : false
      }
      this.tasks.push(newTask)
      this.newTaskTitle = ''
    }
  },
};
</script>
