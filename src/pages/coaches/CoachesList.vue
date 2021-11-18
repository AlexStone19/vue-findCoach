<template>
   <section>
      <coach-filter @change-filter="setFilters"></coach-filter>
   </section>
   <section>
      <base-card>
         List of coaches
         <div class="controls">
            <base-button mode="outline">Refresh</base-button>
            <base-button link to="/register">Register as coach</base-button>
         </div>
         <ul v-if="hasCoaches">
               <coaches-item
                  v-for="coach in filteredCoaches"
                  :key="coach.id"
                  :id="coach.id"
                  :first-name="coach.firstName"
                  :last-name="coach.lastName"
                  :rate="coach.hourlyRate"
                  :areas="coach.areas"
               ></coaches-item>
         </ul>
         <h3 v-else>No coaches</h3>
      </base-card>
   </section>
</template>

<script>
import CoachesItem from "../coaches/CoachItem.vue";
import CoachFilter from "../coaches/CoachFilter.vue";

export default {
   data() {
      return {
         activeFIlters: {
            frontend: true,
            backend: true,
            career: true
         }
      }
   },
   components: {
      CoachesItem,
      CoachFilter
   },
   computed: {
      filteredCoaches() {
         const coaches = this.$store.getters["coaches/coaches"];
         return coaches.filter(coach => {
            if(this.activeFIlters.frontend && coach.areas.includes("frontend")){
               return true;
            }
            if(this.activeFIlters.backend && coach.areas.includes("backend")){
               return true;
            }
            if(this.activeFIlters.career && coach.areas.includes("career")){
               return true;
            }
            return false;
         });
      },
      hasCoaches() {
         return this.$store.getters["coaches/hasCoaches"];
      }
   },
   methods: {
      setFilters(updatedFilters) {
         this.activeFIlters = updatedFilters;
      }
   }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.controls {
  display: flex;
  justify-content: space-between;
}
</style>
