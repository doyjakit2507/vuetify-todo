<template>
  <v-list
    class="pt-0" 
    flat>
    <!-- <taks v-for="taks in $store.state.tasks" 
    :key="taks.id"
    :taks="taks"
    /> -->
    <draggable 
      v-model="tasks" 
      handle=".handle"
      >   <!-- handle ประกาศว่า ถ้าหน้า task มี class handle จะใช้ตัวนั้นในการลาก sort  -->
      <taks v-for="taks in tasks" 
      :key="taks.id"
      :taks="taks"
      />
    </draggable>

    <!-- กรณีไม่ใช้ Drag and drop -->
    <!-- <draggable :list="$store.getters.tasksFilterd" handle=".handle">   handle ประกาศว่า ถ้าหน้า task มี class handle จะใช้ตัวนั้นในการลาก sort  -->
      <!-- <taks v-for="taks in $store.getters.tasksFilterd" :key="taks.id":taks="taks"/> -->
    <!-- </draggable> -->

  </v-list>
</template>

<script>

import draggable from "vuedraggable";
export default {
  computed: {
    tasks: {
      get() {
        return this.$store.getters.tasksFilterd
      },
      set(value) {
        this.$store.dispatch('setTasks', value)
      }
    }
  },
  components: {
      'taks': require('@/components/Todo/Task.vue').default,
      draggable
  }
};
</script>