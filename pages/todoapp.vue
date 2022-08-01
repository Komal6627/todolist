<template>
  <main class="flex justify-center w-full h-screen">
    <div>
      <form
        @submit="formSubmit"
        class=" border-blue-400 rounded-lg border-2 px-12"
      >
        <table>
          <label class="pt-10 py-10" for="taskname">Task name:</label
          ><br />
          <input
            type="text"
            v-model="task.taskname"
            id="taskname"
            name="taskname"
            placeholder="Enter your task"
          /><br /><br />
          <br /><br />
          <div>
            <button
              class="
                py-1
                px-5
                mr-5
                bg-black
                hover:bg-blue-400
                text-white
                font-bold
                text-center
                rounded-md
                mb-3
              "
              type="submit"
              @click="formSubmit"
            >
              Submit
            </button>
            <button
              class="
                py-1
                px-5
                bg-black
                hover:bg-blue-400
                text-white
                font-bold
                text-center
                rounded-md
                mb-3
              "
              type="reset"
            >
              Reset
            </button>
          </div>
        </table>
      </form>
      <br />
      
        <ul v-for="(item, index) in list" v-bind:index="index" :key="item">
          <li class="px-4 border-blue-400 rounded-lg border-4">
            {{ item.taskname }}
            <button
          class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20"
          @click="userDelete(index)"
        >
          Delete
        </button>
        <button
          class="
            mx-3
            rounded-lg
            bg-green-600
            hover:bg-green-600
            text-white
            w-20
          "
          @click="onEdit(index)"
        >
          Edit
        </button>
     
          </li>
        </ul>
        
         </div>
  </main>
</template>
<script>
export default {
  data() {
    return {
      isEdit: false,
      indexEdit: -1,
      list: [],
      task: {
        taskname: " ",
      },
    };
  },
  methods: {
    formSubmit(event) {
      event.preventDefault();
      if (this.isEdit == true) {
        this.list[this.indexEdit] = this.task;
        this.isEdit = false;
        this.indexEdit = -1;
      } else {
        this.list.push(this.task);
      }
      this.task = {
        taskname: " ",
      };
    },
    onReset(event) {
      event.preventDefault();
      this.form.taskname = "";
    },
    userDelete(index) {
      this.list.splice(index, 1);
    },
    onEdit(index) {
      this.task.taskname = this.list[index].taskname;
      this.isEdit = true;
      this.indexEdit = index;
    },
  },
};
</script>
