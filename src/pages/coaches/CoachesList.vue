<template>
   <section>FIlter</section>
   <section>
      List of coaches
      <div class="controls">
         <button>Refresh</button>
         <router-link to="/register">Register as coach</router-link>
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
      </div>
   </section>
</template>

<script>
import CoachesItem from "../coaches/CoachItem.vue";

export default {
   components: {
      CoachesItem
   },
   computed: {
      filteredCoaches() {
         return this.$store.getters["coaches/coaches"];
      },
      hasCoaches() {
         return this.$store.getters["coaches/hasCoaches"];
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
