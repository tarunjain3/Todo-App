<template>
  <div class="container">
    <!-- Heading -->
    <h2 class="text-center mt-5">Todo App</h2>

    <!-- Input -->
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Task Title"
        class="w-100 form-control mr-4"
      />
      <input
        type="text"
        v-model="descriptionVal"
        placeholder="Task Description"
        class="w-100 form-control mr-4"
      />
      <button class="btn btn-warning rounded-0" @click="submitTask">
        Add Task
      </button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <tr><span :class="{ 'line-through': task.status === 'Finished' }">
              {{ task.name }}
            </span></tr>
            <tr>
            <span :class="{ 'line-through': task.status === 'Finished' }">
              {{ task.description }}
            </span></tr>
          </td>
          <td>
            <button
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': task.status === 'To-do',
                'text-success': task.status === 'Finished',
              }"
            >
              {{ task.status }}
            </button>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      descriptionVal: "",
      editedTask: null,
      statuses: ["To-do", "Finished"],

      tasks: [
        {
          name: "Left with API Implementation",
          description: "Description 1",
          status: "To-do",
        },
        {
          name: "Implemented basic to do App part",
          description: "Description 2",
          status: "Finished",
        },
        {
          name: "Implemented Basic UI part",
          description: "Description 3",
          status: "Finished",
        },
      ],
    };
  },

  methods: {
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 1) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.descriptionVal = this.tasks[index].description;
      this.editedTask = index;
    },
    submitTask() {
      if (this.task.length === 0) return;

      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.tasks[this.editedTask].description = this.descriptionVal;
        this.editedTask = null;
      } else {
        this.tasks.push({
          name: this.task,
          description: this.descriptionVal,
          status: "todo",
        });
      }

      this.task = "";
      this.description = "";
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.line-through {
  text-decoration: line-through;
}
</style>