<template>
  <div>
    <v-text-field
      v-model="newtasktitle"
      @click:append="addtask"
      @keyup.enter="addtask"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      class="pa-5"
      clearable
    ></v-text-field>


    <v-list class="pt-0" flat>
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="donetask(task.id)"
          :class="{ 'blue  lighten-5 ': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{
                  'grey--text text-decoration-line-through': task.done,
                }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn @click.stop="updatetask(task.id)" icon>
                <v-icon color="blue">mdi-pencil</v-icon>
              </v-btn>
            </v-list-item-action>
            <v-list-item-action>
              <v-btn @click.stop="deletetask(task.id)" icon>
                <v-icon color="red">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
        <div v-if="task.flag">
      <v-text-field
        v-model="updatetasktitle"
        solo
        clearable
        class="pa-8"
        @keyup.enter="updatetaskmethod(task.id)"
      ></v-text-field>
    </div>
      </div>
    </v-list>

    <!-- <div v-if="alert">
      <v-alert
        v-model="alert"
        border="left"
        close-text="Close Alert"
        color="grey lighten-3"
        dismissible
      >
        New task added
      </v-alert>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "todo",
  data() {
    return {
      newtasktitle: "",
      newtaskadded: false,
      //alert: false,
      updatetasktitle: "Edit Task",
      tasks: [
        {
          id: 1,
          title: "This is your task",
          done: false,
          flag:false
        },
      ],
    };
  },
  methods: {
    donetask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
      console.log(task.id);
    },
    deletetask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    updatetask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.flag = !task.flag;
    },
    updatetaskmethod(id){
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.title = this.updatetasktitle
      task.flag = !task.flag;
      this.updatetasktitle="Edit Task"

    },
    addtask() {
      // console.log('add task')
      let newtask = {
        id: Date.now(),
        title: this.newtasktitle,
        done: false,
        flag:false
      };
      this.tasks.push(newtask);
      this.newtasktitle = "";
      this.alert = true;
      this.updatetasktitle = "Edit Task"
    },
  },
};
</script>




