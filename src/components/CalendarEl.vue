<template>
  <div class="break">
    <section class="calendar">
      <h3 class="title calendar__header">{{ monthIndex + 1 }}</h3>
      <div class="columns is-mobile">
        <div class="column subtitle" v-for="day in days" :key="day">{{ day[0] }}</div>
      </div>
      <div class="columns is-mobile" v-for="(week, weekIndex) in weeks" :key="weekIndex">
        <div class="column" v-for="(day, dayIndex) in week" :key="dayIndex">{{ day }}</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'CalendarEl',
  props: [ // monthDates is an array [dayIndex: dayName]
    'monthDates',
    'monthIndex',
    'year',
    'days',
    'calendarStyle',
  ],
  data() { return {}; },
  computed: {
    weeks() {
      const ret = [];
      // go through every day in the month
      // Make a new
      let dateIndex = 0;
      while (dateIndex < this.monthDates.length) {
        const week = [];
        for (let day = 0; day < 7; day += 1) {
          if (this.monthDates[dateIndex] === this.days[day]) {
            week.push(dateIndex + 1);
            dateIndex += 1;
          } else {
            week.push('');
          }
        }
        ret.push(week);
      }
      return ret;
    },
  },
};
</script>
<style>
.calendar {
  text-align: center;
}
.calendar__header {
  text-align: center;
  margin: 0 auto 30px auto;
}
</style>
