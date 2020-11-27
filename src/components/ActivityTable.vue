<template>
    <div>
        <!-- List of Activity Records TABLE section -->
        <div class="card">
            <h2 class="card-header">Activity Records</h2>

            <div class="card-body">
                <h3>
                    <!-- TODO Display number of records -->
                    {{ totalRecords }}                              <!-- with computed property -->
                    <!-- {{ activityRecords.length }} records       without computed property -->
                </h3>

                <div id="records">
                    <table class="table table-hover">               <!-- START of table -->
                        <tr>
                            <th>Date</th>
                            <th>How many hours?</th>
                            <th>Type</th>
                            <th>Media</th>
                            <th>Completed</th>
                            <th>Notes</th>
                        </tr>

                        <!-- TODO use v-for to create one table row for each activity record -->
                        <!-- v-bind:class creates class identifiers (not dynamic, it is hard coded) for css styling -->
                        <tr v-for="record in activityRecords"
                            v-bind:class="{sketchingRow: record.type === 'Sketching',
                                           drawingRow: record.type === 'Drawing',
                                           paintingRow: record.type === 'Painting'}">
                            <td>{{ record.date | shortDate}}</td>
                            <td>{{ record.hours | decimalPlaces(2)}}</td>
                            <td>{{ record.type }}</td>
                            <td>{{ record.medium }}</td>
                            <td>{{ record.completed | checkedBox}}</td>
                            <td>{{ record.note | textareaDisplayCharacterLimit}}</td>
                        </tr>
                    </table>            <!-- END of table -->
                </div>                  <!-- END of #records div -->
            </div>                      <!-- END of .card-body div -->
        </div>                          <!-- END of List of Activity Records TABLE section -->
    </div>
</template>


<script>
    export default {
        name: "ActivityTable",          // name of component
        // do not modify a prop
        props: {
            activityRecords: Array      // this data has to be provided by its parent, App.vue
        },
        filters: {
            // used in the list of records table
            shortDate(date) {
                return new Intl.DateTimeFormat("en-US", { timeZone: "UTC" }).format(date);
            },
            checkedBox(completed) {
                if(completed)
                {
                    return `Completed`;
                }
                return `Not completed`;
            },
            decimalPlaces: function(hours, numberOfDecimalPlaces) {
                let formattedHours = hours.toFixed(numberOfDecimalPlaces);
                return formattedHours;
            },
            textareaDisplayCharacterLimit(text) {
                if(text.length >= 40)
                {
                    return text.substr(0, 40) + "...";
                }
                return text;
            }
        },
        computed: {
            // set the plurality of the word 'record(s)' in the table section of the application
            totalRecords() {
                if (this.activityRecords.length == 1)
                {
                    return `1 record`;
                }
                else
                {
                  return this.activityRecords.length + " records";
                }
            },
        }
    }
</script>


<style scoped>
    #records
    {
        max-height: 250px;
        overflow: scroll;
    }

    .sketchingRow
    {
        background-color: yellow;
    }

    .drawingRow
    {
        background-color: greenyellow;
    }

    .paintingRow
    {
        background-color: orange;
    }
</style>