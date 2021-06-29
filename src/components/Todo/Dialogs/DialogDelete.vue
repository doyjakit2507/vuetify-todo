<template>
  <v-dialog 
    :value="true"
    persistent max-width="290">

    <v-card>
      <v-card-title 
      class="text-h5">
        Delete task?
      </v-card-title>
      <v-card-text
        >Are you sure to delete task?.</v-card-text
      >
      <v-card-actions>

        <v-spacer></v-spacer>

        <v-btn  
            @click="$emit('close')"
            text   
        >
          NO
        </v-btn>
        <v-btn
            @click="$store.dispatch('deleteTask', taks.id)" 
            color="red darken-1" 
            text 
        >
          YES
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
    props: ['taks']
};
</script>

<style>
</style>