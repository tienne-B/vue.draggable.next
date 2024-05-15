<template>
  <div class="row">
    <div class="col-3">
      <h3>Draggable 1</h3>
      <nested-draggable
        :tasks="list1"
        @update:tasks="list1 = $event"
        group="tasks"
        @change="log"
        :swap="true"
      >
        <template #item="{ element, index }">
          <div class="list-group-item">{{ element.name }} {{ index }}</div>
        </template>
      </nested-draggable>
    </div>

    <div class="col-3">
      <h3>Draggable 2</h3>
      <nested-draggable
        :tasks="list2"
        @update:tasks="list2 = $event"
        group="tasks"
        @change="log"
        :swap="true"
      >
        <template #item="{ element, index }">
          <div class="list-group-item">{{ element.name }} {{ index }}</div>
        </template>
      </nested-draggable>
    </div>

    <rawDisplayer class="col-3" :value="list1" title="List 1" />

    <rawDisplayer class="col-3" :value="list2" title="List 2" />
  </div>
</template>
<script>
import nestedDraggable from "./infra/nested-modelValue";

export default {
  name: "nested-swap",
  display: "Nested swap",
  order: 18,
  components: {
    nestedDraggable
  },
  data() {
    return {
      list1: [
        { name: "A 1", tasks: [{ name: "A 1.1", tasks: [] }] },
        {
          name: "A 2",
          tasks: [
            {
              name: "A 2.1",
              tasks: [
                { name: "A 2.1.1", tasks: [] },
                { name: "A 2.1.2", tasks: [] }
              ]
            }
          ]
        }
      ],
      list2: [
        { name: "B 1", tasks: [{ name: "B 1.1", tasks: [] }] },
        {
          name: "B 2",
          tasks: [
            {
              name: "B 2.1",
              tasks: [
                { name: "B 2.1.1", tasks: [] },
                { name: "B 2.1.2", tasks: [] }
              ]
            }
          ]
        }
      ]
    };
  },
  methods: {
    log: function(evt) {
      window.console.log(evt);
    }
  }
};
</script>
