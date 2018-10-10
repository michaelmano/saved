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
      quitDate: 1539122894,
      now: moment().unix(),
      costPerMinute: 0.02060185185,
    };
  },
  computed: {
    minutesSince() {
      return ((this.now - this.quitDate) / 60).toFixed(0);
    },
    savings() {
      return (this.costPerMinute * this.minutesSince).toFixed(2);
    },
    liveTime() {
      const mins = `${(this.now - this.quitDate) / 60}`.split('.')[0];
      return `${Math.floor(mins / 60)} hours, ${mins % 60} minutes ago`;
    },
  },
  methods: {
    formatDateTime(epoc) {
      const dateTime = moment.unix(epoc)
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
  color: #ffffff;
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
