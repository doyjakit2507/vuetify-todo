<template>
  <div>
    <v-list-item
      @click="$store.dispatch('doneTask', taks.id)"
      :class="{ 'blue lighten-5': taks.done }"
      class="white"
      :ripple="false"
    >
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox :input-value="taks.done" color="primary"> </v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title
            :class="{ 'text-decoration-line-through': taks.done }"
            >
            {{ taks.title }}
          </v-list-item-title>
        </v-list-item-content>

        <v-list-item-action
          v-if="taks.dueDate"
        >
          <v-list-item-action-text>
            <v-icon small>
              mdi-calendar
            </v-icon>
          {{ taks.dueDate | niceDate}}
          </v-list-item-action-text>
        </v-list-item-action>

        <v-list-item-action>
          <!-- <v-btn @click.stop="$store.dispatch('deleteTask', taks.id)" icon> -->
          <!-- <v-btn 
            @click.stop="dialogs.delete = true"
            icon>
            <v-icon color="primary lighten-1">mdi-delete</v-icon>
          </v-btn> -->
          <task-menu 
            :taks="taks"
          />
        </v-list-item-action>
          
        <v-list-item-action
          v-if="$store.state.sorting">
            <v-btn
              color="primary"
              class="handle"   
              icon>
              <v-icon> <!--handle เพื่อให้หน้า ListTask.vue รู้ว่าจะใช้ class ไหนเป็นตัว sort-->
                mdi-drag-horizontal-variant
              </v-icon>
          </v-btn>
        </v-list-item-action>
      </template>
    </v-list-item>
    <v-divider></v-divider>
 
  </div>
</template>

<script>

import { format } from 'date-fns'

export default {
    props: ['taks'],
    filters: {
      niceDate(value) {
        return format(new Date(value), 'MMM d')
      }
    },
    components: {
      'task-menu': require('@/components/Todo/TaskMenu.vue').default
    }
};
</script>

<style lang="sass">
  .sortable-ghost
    opacity: 0

  .sortable-drag
    box-shadow: 0 0 10px rgba(0,0,0,0.3)

</style>