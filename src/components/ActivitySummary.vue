<template>
    <div>
        <!-- Activity Summary section -->
        <div class="card">
            <h2 class="card-header">Summary</h2>

            <div class="card-body">
                <!-- TODO add computed property to calculate the total hours -->
                <p>
                    You have practiced a total of
                    <!-- TODO display total hours -->
                    <!-- a computed property used with a filter -->
                    {{ totalHours | decimalPlaces(2) }} hours.
                </p>

                <!-- Challenge question! Display a list of the total hours for each type.  -->
                <p v-if="activityRecords.length != 0">
                    Practice hours for each activity:
                    <li v-for="eachActivityHours in totalHoursForEachActivityRecord">
                        {{eachActivityHours.typeOfActivity}}: {{ eachActivityHours.numOfHours | decimalPlaces(2)}}
                    </li>
                </p>
            </div>      <!-- END of .card-body div -->
        </div>          <!-- END of the activity summary section -->
    </div>
</template>


<script>
    export default {
        name: "ActivitySummary",            // name of the component
        props: {
            // this data has to be provided by its parent, App.vue
            activityRecords: Array,
            types: Array                    // ASK PROF: DO WE NEED THIS HERE?
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
            },
            totalHoursForEachActivityRecord() {
                let arrayOfObjects = [];                            // empty array for objects
                // empty object for each type and hours for the type ("object literal" syntax)
                let objectInArray = {};

                this.activityRecords.forEach( record => {
                    this.types.forEach( activityType => {
                        // if the record entered is equal to one of the activity types
                        if(record.type === activityType)
                        {
                            // if there are no items/objects in the arrayOfObjects
                            if(arrayOfObjects.length === 0)
                            {
                                // create a new object
                                objectInArray = {
                                    typeOfActivity: record.type,
                                    numOfHours: record.hours
                                }

                                // push the object on to the arrayOfObjects
                                arrayOfObjects.push(objectInArray);
                            }
                            // else if there are items/objects in the arrayOfObjects,
                            // i.e., arrayOfObjects.length != 0
                            else
                            {
                                let found = false;      // initial boolean to record not found

                                // loop through the array to find if the item/object already exists
                                for(let i = 0; i < arrayOfObjects.length; i++)
                                {
                                    // if the record exists in the arrayOfObjects
                                    if(record.type === arrayOfObjects[i].typeOfActivity)
                                    {
                                        // then just update the number of hours for that item/object
                                        arrayOfObjects[i].numOfHours += record.hours;
                                        found = true;           // record is found
                                    }
                                }

                                // if the record is not found in the arrayOfObjects
                                if(!found)
                                {
                                    // create a new object
                                    objectInArray = {
                                        typeOfActivity: record.type,
                                        numOfHours: record.hours
                                    }

                                    // push the object on to the arrayOfObjects
                                    arrayOfObjects.push(objectInArray);
                                }
                            }
                        }
                    })              // end of types array forEach
                })                  // end of activityRecords array forEach

                return arrayOfObjects;
            }                                               // END of the totalHoursForEachActivityRecord
        }
    }
</script>


<style scoped>

</style>