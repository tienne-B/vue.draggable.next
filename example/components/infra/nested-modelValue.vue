<template>
  <draggable
    class="dragArea"
    v-model="tasks2"
    :group="{ name: 'g1' }"
    item-key="name"
  >
    <template #item="{ element, index }">
      <div>
        <p>{{ element.name }}</p>
        <div>
          <nested-draggable
            :tasks="element.tasks"
            @update:tasks="update($event, index)"
            v-bind="$attrs"
          />
        </div>
      </div>
    </template>
  </draggable>
</template>
<script>
import draggable from "@/vuedraggable";

export default {
  props: {
    tasks: {
      required: true,
      type: Array
    }
  },
  components: {
    draggable
  },
  name: "nested-draggable",
  emits: ["update:tasks"],
  computed: {
    tasks2: {
      get() {
        return [...this.tasks];
      },
      set(val) {
        this.$emit("update:tasks", val);
      }
    }
  },
  methods: {
    update(val, index) {
      const newTasks = [...this.tasks];
      newTasks[index].tasks = val;
      this.$emit("update:tasks", newTasks);
    }
  }
};
</script>
<style scoped>
.dragArea {
  min-height: 50px;
  outline: 1px dashed;
}
</style>
