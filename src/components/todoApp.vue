<template>
  <div class="container">
    <h1 class="mb-5">My To-Do Application</h1>
    <div class="d-flex mb-5">
      <input
        type="text"
        class="form-control rounded-0"
        placeholder="Write a new task !"
        v-model="newTask"
        @keyup.enter="addTask"
      />
      <button
        class="btn btn-warning rounded-0 border border-secondary"
        style="width: 150px"
        @click="addTask"
      >
        + Add Task
      </button>
    </div>

    <div>
      <table class="table table-bordered">
        <thead>
          <tr>
            <th scope="col" style="width: 700px">Task</th>
            <th scope="col" style="width: 250px">Status</th>
            <th scope="col">#</th>
            <th scope="col">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todoTask, index) in todoTasks" :key="index">
            <td :class="{'finished': todoTask.status === 'Finished'}">{{ todoTask.task }}</td>
            <td
              class="pointer"
              @click="changeStatus(index)"
              :class="{
                'text-danger': todoTask.status === 'To-do',
                'text-warning': todoTask.status === 'In-progress',
                'text-success': todoTask.status === 'Finished',
              }"
            >
              {{ todoTask.status }}
            </td>
            <td class="pointer" @click="deleteTask(index)">
              <b-icon icon="trash-fill" variant="dark"></b-icon>
            </td>
            <td class="pointer" @click="EditTask(index)">
              <b-icon icon="pencil-fill" variant="dark"></b-icon>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {},
  data() {
    return {
      todoTasks: [
        { task: "Clean the Room !", status: "To-do" },
        { task: "Eat the Dinner Right at 8 o'clock !", status: "Finished" },
      ],
      newTask: "",
      editedTask: null,
      availableStatus: ["To-do", "In-progress", "Finished"],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.length === 0) return;
      if (this.editedTask === null) {
        this.todoTasks.push({
          task: this.newTask,
          status: "To-do",
        });
      } else {
        this.todoTasks[this.editedTask].task = this.newTask;
        this.editedTask = null;
      }
      this.newTask = "";
    },
    deleteTask(index) {
      this.todoTasks.splice(index, 1);
    },
    EditTask(index) {
      this.newTask = this.todoTasks[index].task;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.availableStatus.indexOf(this.todoTasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.todoTasks[index].status = this.availableStatus[newIndex];
    }
  },
};
</script>
<style scoped>
.btn:focus,
.form-control:focus {
  box-shadow: none;
}
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
}
</style>
