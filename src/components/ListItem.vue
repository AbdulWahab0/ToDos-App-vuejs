<template>
  <tr>
    <td>
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
      <span class="icon-delete" @click="onTaskDelete"></span>
    </td>

    <td>
      {{ priority }}
    </td>

    <td>
      {{ owner }}
    </td>
  </tr>
</template>

<script>
export default {
  name: "ListItem",
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
</style>
