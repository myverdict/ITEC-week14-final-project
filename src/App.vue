<template>
    <div id="app">
        <new-activity-form v-on:record-added="newRecordAdded"></new-activity-form>

        <activity-table v-bind:activityRecords="activityRecords"></activity-table>

        <activity-summary v-bind:activityRecords="activityRecords"></activity-summary>
    </div>
</template>


<script>
    import NewActivityForm from "@/components/NewActivityForm.vue";
    import ActivityTable from "@/components/ActivityTable.vue";
    import ActivitySummary from "@/components/ActivitySummary.vue";

    export default {
        name: 'App',
        components: {
            NewActivityForm,
            ActivityTable,
            ActivitySummary
        },
        data() {
            return {
                // Array of activity records displayed in the activity table summary
                activityRecords: [],
                types: []                     // ASK PROF: HOW TO GET THE TYPES HERE?
            }
        },
        methods: {
            newRecordAdded(record) {
                // Push the record on to the activityRecords array
                this.activityRecords.push(record);

                // sort the records according to date
                this.activityRecords.sort(function(r1, r2) {
                    // returns negative value to order r1 before r2
                    // returns positive value to order r1 after r2
                    // return r1.date.getTime() - r2.date.getTime();        // earliest records at the beginning of the list
                    return r2.date.getTime() - r1.date.getTime();           // recent records at the beginning of the list
                })
            }
        }
    }
</script>


<style>

</style>
