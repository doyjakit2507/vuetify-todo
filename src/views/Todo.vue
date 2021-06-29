<template>
  <div class="home">
                              <!-- component add task -->
    <list-task v-if="$store.state.tasks.length" />  <!-- component list task -->
    <no-task v-else />      
    <button-done-sorting 
      v-if="$store.state.sorting"
    />                        <!-- component no task -->
  </div>
</template>

<script>
// import FieldAddTask from '@components/Todo/FieldAddTask.vue'

export default {
  name: "Home",
  components: {
    // 'field-add-task': FieldAddTask
    "list-task": require("@/components/Todo/ListTasks.vue").default,
    "no-task": require("@/components/Todo/NoTasks.vue").default,
    "button-done-sorting": require("@/components/Todo/ButtonDoneSorting.vue").default,
    
  },
};
</script>

