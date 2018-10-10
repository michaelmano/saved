<template>
  <div id="app">
    <h1>I have saved ${{ savings }}</h1>
    <p>{{ formatDateTime(quitDate) }} was my last cigarette.</p>
    <h3>That was {{ liveTime }}.</h3>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'app',
  data() {
    return {
      quitDate: moment.unix(1539122894),
      now: moment(),
      costPerMinute: 0.02060185185,
      liveTime: 'loading...',
    };
  },
  mounted() {
    setInterval(() => {
      this.liveTime = moment(this.quitDate.diff(moment())).format('hh [hours] m [minutes and ] ss [ seconds ago]');
    }, 1000);
  },
  computed: {
    minutesSince() {
      const DIFF = moment(this.now.diff(this.quitDate));
      const HOURS = DIFF.format('h') * 60;
      const MINUTES = DIFF.format('m');
      return parseInt(HOURS, 0) + parseInt(MINUTES, 0);
    },
    savings() {
      return (this.costPerMinute * this.minutesSince).toFixed(2);
    },
  },
  methods: {
    formatDateTime(dateTime) {
      return `${dateTime.format('dddd')} ${this.ordinal(dateTime.format('DD'))} of ${dateTime.format('MMMM YYYY')} at ${dateTime.format('h:hha')}`;
    },
    ordinal(number) {
      switch (number) {
        case 1:
        case 21:
          return `${number}st`;
        case 2:
        case 22:
          return `${number}nd`;
        case 3:
        case 23:
          return `${number}rd`;
        default:
          return `${number}th`;
      }
    },
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Kodchasan|Lato');
*,
*:before,
*:after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
p {
    margin-bottom: 1rem;
}
body,
html {
  font-family: 'Lato', sans-serif;
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
  padding: 1.25rem;
  background-color: rgb(66, 66, 80);
  color: #FFFFFF;
  text-align: center;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: 'Kodchasan', sans-serif;
  margin-bottom: 1rem;
}
h3 {
  color: rgb(253, 171, 47);
}
</style>
