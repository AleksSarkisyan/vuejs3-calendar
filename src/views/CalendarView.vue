<script>
  import { onMounted, computed, defineComponent, ref } from 'vue';
  import useHours from '../hooks/useHours.vue';
  import useAxios from '../hooks/useAxios.vue';
  import useHoursEvents from '../hooks/useHoursEvents.vue';
  import TitleComponent from "../components/TitleComponent.vue";
  import CalendarComponent from "../components/CalendarComponent.vue";

  export default defineComponent({
    name: 'CalendarView',
    components: { TitleComponent, CalendarComponent },
    setup() {
      const { getHours } = useHours();
      const { get } = useAxios();

      let hourlyEvents = ref([]);

      onMounted(async () => {
        let events = await get("events");

        if(!events.data) {
          console.log('No events found!');
          return false;
        }
        
        const { prepareHourEvents } = useHoursEvents(getHours(), events.data);
        hourlyEvents.value = prepareHourEvents().hours;
      });
      
      const calendarTitle = computed(() => {
        return 'Jiminny Calendar';
      })

      return {
        hourlyEvents,
        calendarTitle
      }
    }
  });

</script>

<template>
  <div class="calendar-wrapper">
    <TitleComponent :title="calendarTitle"/>
    <CalendarComponent 
      v-if="hourlyEvents.length"
      :hourlyEvents="hourlyEvents"
    />
  </div>
</template>

<style scoped>

</style>
