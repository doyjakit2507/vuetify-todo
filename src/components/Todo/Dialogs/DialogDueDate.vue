<template>
  <v-dialog
        ref="dialog"
        :value="true"
        :return-value.sync="date"
        persistent
        width="290px"
        >
        <v-date-picker
            v-model="date"
            scrollable
        >
            <v-spacer></v-spacer>
            <v-btn
            text
            color="primary"
            @click="$emit('close')"
            >
            Cancel
            </v-btn>
            <v-btn
            @click="saveTask"
            text
            color="primary"
            >
            OK
            </v-btn>
        </v-date-picker>
    </v-dialog>
</template>

<script>
export default {
    props: ['taks'],
    data() {
        return {
            date: null
        }
    },
    mounted() {
        if (this.taks.dueDate) {
            this.date = this.taks.dueDate
        }
    },
    methods: {
        saveTask() {
            let payload = {
                id: this.taks.id,
                dueDate: this.date
            }
            this.$store.dispatch('updateTaskDueDate', payload)
            this.$emit('close')
        }
    }
}
</script>

<style>

</style>