<script>
  import { defineComponent } from 'vue';
  import EventItem from "../components/EventItem.vue";
  import "../assets/calendar.css";

  export default defineComponent({
    name: 'CalendarComponent',
    components: { EventItem },
    props: {
      hourlyEvents: {
        type: Array,
        required: true
      }
    },
    setup(props) {
      const isLastHour = (index, hourlyEvents) => {
        return index == hourlyEvents.length -1;
      }

      const isFirstHour = (index) => {
        return index == 0;
      }

      return {
        hourlyEvents: props.hourlyEvents,
        isLastHour,
        isFirstHour
      }
    },
  })
</script>

<template>
  <div class="calendar">
    <div class="hour-item" v-for="(hourEvent, index) in hourlyEvents" :key="index">
      <span class="time">{{ hourEvent.hour }}</span>
      <span 
        class="separator" 
        :class="{first: isFirstHour(index)}"
      >
      </span>

      <div 
        class="events" 
        :class="{last: isLastHour(index, hourlyEvents)}"
      >
        <EventItem 
          :hourEvent="hourEvent" 
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
 
</style>
