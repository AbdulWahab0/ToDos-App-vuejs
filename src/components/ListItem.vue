<template>
  <tr :class="{ 'list-item--checked': isDone }">
    <td>
      <div class="todo-item">
        <div class="todo-item__left">
          <input
            type="checkbox"
            class="checkbox"
            :id="idComputed"
            @change="onTaskStatusChange"
            :checked="isDone"
          />
          <label class="mr-3" :for="idComputed"></label>
          <span class="text">
            {{ text }}
          </span>
        </div>
        <div class="todo-item__right" @click="onTaskDelete">
          &times;
        </div>
      </div>
    </td>

    <td>
      <div class="priority">
        <div :class="'priority__letter priority__letter--' + priority">
          {{ priority }}
        </div>

        <div class="priority__text">
          {{ priorityText[priority] }}
        </div>
      </div>
    </td>

    <td class="text-center">
      <div class="owner">
        {{ owner }}
      </div>
    </td>
  </tr>
</template>

<script>
export default {
  name: "ListItem",
  data: () => ({
    priorityText: {
      A: "Very High",
      B: "High",
      C: "Moderate",
      D: "Low"
    }
  }),
  props: {
    id: {
      type: Number,
      default: 0
    },
    text: {
      type: String,
      default: ""
    },
    isDone: {
      type: Boolean,
      default: false
    },
    priority: {
      type: String,
      default: ""
    },
    owner: {
      type: String,
      default: ""
    }
  },
  computed: {
    idComputed() {
      return `item-${this.id}`;
    }
  },
  methods: {
    /**
     * Event: on task status changed
     */
    onTaskStatusChange(e) {
      const checked = e.target.checked;
      this.$emit("eventTaskStatusChange", this.id, checked);
    },

    /**
     * Event: on task deleted
     */
    onTaskDelete(e) {
      this.$emit("eventTaskDelete", this.id);
    }
  }
};
</script>

<style>
tr:hover .icon-delete {
  visibility: visible;
}

.list-item--checked .text {
  text-decoration: line-through;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.todo-item__left {
  display: flex;
  align-items: center;
}

.todo-item__right {
  font-size: 28px;
  font-weight: bold;
  visibility: hidden;
  cursor: pointer;
  color: red;
}

.todo-item:hover .todo-item__right {
  visibility: visible;
}

.priority {
  width: 122px;
  display: flex;
  align-items: center;
  background-color: #ebedef;
  border-radius: 44px;
  font-size: 13px;
}

.priority__letter {
  font-weight: bold;
  border-radius: 55px;
  color: #fff;
  padding: 2px 14px;
  font-size: 20px;
}

.priority__text {
  padding: 0 8px;
}

.priority__letter--A {
  background-color: #c8343d;
}

.priority__letter--B {
  background-color: #e36335;
}

.priority__letter--C {
  background-color: #fc953b;
}

.priority__letter--D {
  background-color: #fcae3f;
}

.owner {
  background-color: #08334b;
  color: #fff;
  width: 39px;
  height: 39px;
  border-radius: 39px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
}
</style>
