<script>
  import { defineComponent } from 'vue';
  import "../assets/event.css";

  export default defineComponent({
    name: 'EventItem',
    props: {
      hourEvent: {
        type: Object,
        required: true
      }
    },
    setup(props) {  
      /** Calculates event height and start position */
      const getEventStyles = (event, hourEvent) => {
        let eventDuration = event.event[0].endTime - event.event[0].startTime;
        let startPosition = 0;

        if (eventDuration < 30) {
          eventDuration = '30';
        }

        /** Fixes overlapping events */
        if (event.event[0].hasOverlap) {
          eventDuration = '60';
        }

        startPosition = (event.event[0].startTime - hourEvent.minutes);

        if (hourEvent.minutes > 60) {
          startPosition = (event.event[0].startTime - hourEvent.minutes + 1);
        }

        if (startPosition <= -1) {
          startPosition = 0;
        }

        return {
          height: eventDuration + 'px',
          marginTop: startPosition + 'px'
        }
      }

      return {
        hourEvent: props.hourEvent,
        getEventStyles
      }
    }
  });

</script>

<template>
  <div class="event"
    v-for="(event, eventIndex) in hourEvent.events"
    :key="eventIndex"
    :style="getEventStyles(event, hourEvent)"
  >
    <div class="event-title">Event Title</div>
  </div>
</template>

<style scoped>

</style>
