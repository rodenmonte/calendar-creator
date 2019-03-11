<template>
  <div>
    <header-hero></header-hero>
    <div class="columns is-centered">
      <div class="column is-4">
        <b-field label="Calendar Year">
          <b-input type="number" v-model="calendarYear"></b-input>
        </b-field>
        <a @click="print" class="button is-primary">
          <span class="icon is-small">
            <i class="fa fa-print"></i>
          </span>
          &nbsp;&nbsp;
          Print
        </a>
      </div>
      <div class="column is-6">
        <div id="calendar-container" class="calendar-container">
        <calendar-el
          v-for="(monthDates, index) in calendarMonths"
          :key="index"
          :monthDates="monthDates"
          :monthIndex="index"
          :days="days"
          :year="calendarYear"
        />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderHero from './HeaderHero';
import CalendarEl from './CalendarEl';

export default {
  name: 'CalendarCreator',
  data() {
    return {
      calendarYear: new Date().getYear() + 1900,
      days: ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'],
    };
  },
  computed: {
    calendarMonths() {
      const result = [];
      for (let month = 0; month < 12; month += 1) {
        result.push([]); // Hold the month-th month
        const daysInMonth = new Date(this.calendarYear, month + 1, 0).getDate();
        for (let day = 0; day < daysInMonth; day += 1) {
          result[month].push(this.days[new Date(this.calendarYear, month, day + 1).getDay()]);
        }
      }
      return result;
    },
  },
  components: {
    HeaderHero,
    CalendarEl,
  },
  methods: {
    print() {
      window.print();
    },
  },
};
</script>

<style>
/* All the print style's here for simplicity */
@media print {
  @page { margin: 0; }
  body {
    visibility: hidden;
    margin: 1.6cm;
  }
  #calendar-container {
    visibility: visible;
    margin: 0;
    padding: 0;
    position: absolute;
    top: 0;
    left: 0;
    width:100vw;
    height:100vh;
    overflow: visible;
  }
  .break {
    page-break-after: always;
    position: relative;
  }
  .calendar {
    width: 100vw;
    height: 100vh;
    margin: 0 auto;
    padding: 32px;
    text-align: center;
    page-break-after: always;
  }
  .calendar .title {
    margin: 164px 0 128px 0;
  }
  .calendar .columns {
    margin: 24px 0 24px 0;
  }
}
.calendar-container {
  max-height: 70vh;
  overflow-y: auto;
  overflow-x: hidden;
}
</style>
