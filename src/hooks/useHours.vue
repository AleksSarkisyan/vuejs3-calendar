<script>

import hours from "../../hours";

export default function useHours() {
  /** Adds some useful properties to the hours, so that we can determine which events would fall in an hour */
  const getHours = () => {
    hours.forEach((hour, index) => {
      hour.maxMinutes = calculateHourMinutes({ index, isMaxMinutes: true });
      hour.minutes = calculateHourMinutes({ index, isMaxMinutes: false });
      hour.events = [];
      if (index > "0") {
        hour.minutes = index * 60 + 1;
      }
    });

    return hours;
  };

  const calculateHourMinutes = (params) => {
    const { index, isMaxMinutes } = { ...params };
    const hourMinutes = 60;

    if (isMaxMinutes) {
      return hourMinutes + index * hourMinutes;
    }

    return index * hourMinutes;
  };

  return {
    getHours
  };
}
</script>
