<template>
  <div>
    <div class="row justify-content-between">
      <div class="col-4">
        <h2 class="mb-4">ToDo</h2>
      </div>
      <div class="col-auto">
        <button class="add-new" @click="addModal = true">Add new</button>
      </div>
    </div>
    <div class="ani-slideInDown row justify-content-center">
      <div class="col-lg-12">
        <table class="table table-bordered my-table mt-3">
          <thead>
            <tr>
              <th scope="col" class="column-title">Title</th>
              <th scope="col" class="column-priority">Priority</th>
              <th scope="col" class="column-owner">Owner</th>
            </tr>
          </thead>
          <tbody>
            <!-- <tr>
            <th>title</th>
            <td>ppp</td>
            <td>www</td>
          </tr> -->
            <ListItem
              v-for="item in itemList"
              :key="item.id"
              :text="item.text"
              :id="item.id"
              :isDone="item.isDone"
              :priority="item.priority"
              :owner="item.owner"
              @eventTaskStatusChange="onTaskStatusChange"
              @eventTaskDelete="onTaskDelete"
            />
          </tbody>
        </table>

        <!-- <ul class="list mt-3">
        <ListItem
          v-for="item in itemList"
          :key="item.id"
          :text="item.text"
          :id="item.id"
          :isDone="item.isDone"
          @eventTaskStatusChange="onTaskStatusChange"
          @eventTaskDelete="onTaskDelete"
        />
      </ul> -->
      </div>

      <amodal title="Add New Item" v-model="addModal" width="500px">
        <ToDoInput @eventAddNewTask="onAddNewTask" />
      </amodal>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import ToDoInput from "@/components/ToDoInput.vue";
import ListItem from "@/components/ListItem.vue";
import Amodal from "@/components/Amodal.vue";

export default {
  name: "home",
  components: {
    ToDoInput,
    ListItem,
    Amodal
  },
  data() {
    return {
      itemList: [],
      addModal: false
    };
  },
  methods: {
    /**
     * Event: add new task
     */
    onAddNewTask(taskObj) {
      const task = {
        id: new Date().getTime(),
        text: taskObj.text,
        isDone: false,
        priority: taskObj.priority,
        owner: taskObj.owner
      };

      this.itemList.push(task);
      this.addModal = false;
    },

    /**
     * Event: on task status changed
     */
    onTaskStatusChange(id, checked) {
      console.log(id, checked);

      let item = this.itemList.find(i => i.id == id);
      if (item) {
        item.isDone = checked;
      }

      console.log(this.itemList);
    },

    /**
     * Event: on task deleted
     */
    onTaskDelete(id) {
      console.log(id);

      let index = this.itemList.findIndex(i => i.id == id);
      if (index > -1) {
        this.itemList.splice(index, 1);
      }

      console.log(this.itemList);
    },

    /**
     * Load item list from local storage
     */
    loadItemList() {
      this.itemList = JSON.parse(localStorage.getItem("VuejsTodo")) || [];

      console.log("this.itemList =", this.itemList);
    },

    /**
     * Update the item list to local storage
     */
    updateItemList() {
      localStorage.setItem("VuejsTodo", JSON.stringify(this.itemList));
    }
  },
  mounted() {
    // Load item list from local storage
    this.loadItemList();
  },
  watch: {
    itemList: {
      handler(value) {
        console.log("item changed");

        // save to localStorage
        this.updateItemList();
      },
      deep: true
    }
  }
};
</script>

<style>
.my-table {
  width: 100%;
  background-color: #fff;
}

.my-table td,
.my-table th {
  background-color: #fff;
  border: 1px solid #dcdcdc;
}

.my-table th {
  color: #879ba8;
}

.my-table td {
  color: #315064;
}

.column-priority {
  width: 144px;
}

.column-owner {
  width: 71px;
}

button.add-new {
  background-color: #c8343d;
  color: #fff;
  padding: 13px 14px;
  border-radius: 4px;
  border: none;
  font-weight: bold;
  cursor: pointer;
}

button.add-new:hover {
  background-color: #b3222c;
}
</style>
