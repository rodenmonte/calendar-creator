<template>
  <div>
    <calendar-creator/>
  </div>
</template>

<script>
import CalendarCreator from './components/CalendarCreator';

export default {
  name: 'App',
  components: {
    CalendarCreator,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Open+Sans+Condensed:300');
* {
  font-family: 'Open Sans Condensed', sans-serif;
}
</style>
