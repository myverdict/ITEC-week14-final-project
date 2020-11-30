<template>
    <div>
        <!-- Activity Summary section -->
        <div class="card">
            <h2 class="card-header">Summary</h2>

            <div class="card-body">
                <p>
                    You have practiced a total of
                    <!-- a computed property 'totalHours' to calculate the total hours practiced -->
                    <!-- used with a filter to restrict to 2 decimal places -->
                    {{ totalHours | decimalPlaces(2) }} hours.
                </p>

                <!-- Challenge question! Display a list of the total hours for each type. -->

          </div>
      </div>          <!-- END of the activity summary section -->
    </div>
</template>


<script>
    export default {
        name: "ActivitySummary",            // name of the component
        props: {
            activityRecords: Array
        },
        filters: {
            decimalPlaces: function(hours, numberOfDecimalPlaces) {
                let formattedHours = hours.toFixed(numberOfDecimalPlaces);
                return formattedHours;
            }
        },
        computed: {
            // calculate total hours in the summary section of the application
            totalHours() {
                let total = 0;
                this.activityRecords.forEach( record => {
                    total = total + record.hours;                   // alternate: total += record.hours;
                })
                return total;
            }
        }
    }
</script>


<style scoped>

</style>