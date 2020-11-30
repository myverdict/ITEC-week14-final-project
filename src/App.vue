<template>
    <div id="app">
        <new-activity-form v-on:record-added="newRecordAdded"></new-activity-form>

        <activity-table v-bind:activityRecords="activityRecords"
                        v-on:delete-record-table="deleteRecord"
                        v-on:update-record-table="updateRecord">
        </activity-table>

        <activity-summary></activity-summary>
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
                // types: [],                      // ASK PROF: HOW TO GET THE TYPES HERE?
                // mostRecentRecord: {}            // ASK PROF: If we need this for ActivitySummary.vue page
            }
        },
        methods: {
            newRecordAdded(record) {
                // Push the record on to the activityRecords array
                this.activityRecords.push(record);

                // set the mostRecentRecord to current record
                // this.mostRecentRecord = record;            // ASK PROF: If we need this for ActivitySummary.vue page

                // sort the records according to date
                this.activityRecords.sort(function(r1, r2) {
                    // returns negative value to order r1 before r2
                    // returns positive value to order r1 after r2
                    // return r1.date.getTime() - r2.date.getTime();        // earliest records at the beginning of the list
                    return r2.date.getTime() - r1.date.getTime();           // recent records at the beginning of the list
                })
            },
            deleteRecord(record) {
                // filter returns a new array of all records for which the function returns true
                this.activityRecords = this.activityRecords.filter( function (rec) {
                    if (rec != record)
                    {
                        return true;
                    }
                })
            },
            updateRecord() {
                // find the record in this.activityRecords, set completed value
                let updatedRecord = this.activityRecords.find( function (rec) {

                })
            }
        }
    }
</script>


<style>

</style>
