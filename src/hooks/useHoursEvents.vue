<script>

/** Loops thorugh all hours and events and determines which event will belong to which hour */
export default function useHoursEvents(hours, events) {
  const prepareHourEvents = () => {
    let nextEvents = [];
    Object.entries(hours).forEach(([hourKey, hourValue]) => {
      Object.entries(events).forEach(([eventKey, eventValue]) => {
        if (shouldAddEventToHour(eventValue, hourValue)) {
          nextEvents = events.slice(eventKey, -1);

          let hasOverlap = nextEvents.find(nextEvent => {
            return nextEvent.endTime > eventValue.startTime
          });
          
          if (hasOverlap) {
            eventValue.hasOverlap = true;
          }

          let event = [];
          event.push(eventValue);
        
          hourValue.events.push({
            hour: hourValue.hour,
            minutes: hourValue.minutes,
            event
          });
        }
      });
    });
    
    return {
      hours
    };
  };

  /** Checks if an event startTime falls between the minutes of a specific hour */
  const shouldAddEventToHour = (event, hour) => {
    return event.startTime + 1 >= hour.minutes && event.startTime + 1 <= hour.maxMinutes
  }

  return {
    prepareHourEvents
  };
}
</script>
