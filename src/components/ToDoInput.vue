<template>
  <form @submit="onAddNewTask">
    <div class="form-group">
      <input
        type="text"
        placeholder="What needs to be done?"
        v-model="text"
        required
        class="form-control"
      />

      <select class="form-control" v-model="priority" required>
        <option value="">--Priority--</option>
        <option>Very High</option>
        <option>High</option>
        <option>Moderate</option>
        <option>Low</option>
      </select>

      <input
        type="text"
        placeholder="Owner"
        v-model="owner"
        required
        class="form-control mt-4"
      />
      <button type="submit">Add</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "ToDoInput",
  data() {
    return {
      text: "",
      priority: "",
      owner: ""
    };
  },
  methods: {
    /**
     * Event: add new task
     */
    onAddNewTask(e) {
      e.preventDefault();
      const taskName = this.text;

      this.$emit("eventAddNewTask", {
        text: this.text,
        priority: this.priority,
        owner: this.owner
      });

      // reset the textbox
      this.text = "";
    }
  }
};
</script>
