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
      <br />

      <input
        type="text"
        placeholder="Owner"
        v-model="owner"
        required
        class="form-control mt-4"
      />
      <br />
      <select class="form-control mt-4" v-model="priority" required>
        <option value="">--Priority--</option>
        <option value="A">Very High</option>
        <option value="B">High</option>
        <option value="C">Moderate</option>
        <option value="D">Low</option>
      </select>
      <br />

      <button type="submit" class="btn mt-4">Add</button>
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
