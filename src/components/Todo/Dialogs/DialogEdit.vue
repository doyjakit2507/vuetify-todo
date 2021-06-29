<template>
  <v-dialog 
    :value="true"
    persistent max-width="290">

    <v-card>
      <v-card-title 
      class="text-h5">
        Edit task?
      </v-card-title>
      <v-card-text>
        Edit the title of this task: 
        <v-text-field 
          v-model="taskTitle"  
          @keyup.enter="saveTask"
        />
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn  
          @click="$emit('aaa')"
          text   
        >
          CANCEL
        </v-btn>
        <v-btn
            @click="saveTask" 
            color="red darken-1" 
            text 
            :disabled="!taskTitle || taskTitle === taks.title"
        >
          SAVE
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
    props: ['taks'],
    data() {
      return {
        taskTitle: null,
      }
    },
    mounted() {
      this.taskTitle = this.taks.title
    },
    computed: {
      taskTitleInvalid() {
        return !this.taskTitle || this.taskTitle === this.taks.title
      },
      logJa() {
        return console.log("aaa");
      }
    },
    methods: {
      saveTask() {
        if(!this.taskTitleInvalid) {
          let payload = {
            id: this.taks.id,
            title: this.taskTitle
          }
          this.$store.dispatch('updateTaskTitle', payload)
          this.$emit('aaa')
          this.$vuetify.goTo(0, {duration: 0})
        }
      }
    }
};
</script>

<style>
</style>