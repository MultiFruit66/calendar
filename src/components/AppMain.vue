<template>
  <ul class="dayList">
    <li class="day" v-for="(day, index) in days" :key="`a${ index }`">{{ day }}</li>
    <li class="day" v-for="(day, index) in startFrom" :key="`b${ index }`"></li>
    <li class="day" :class="{today: day === currentDay}" 
      v-for="(day, index) in countOfDays" :key="`c${ index }`">{{ day }}</li>
  </ul>
</template>

<script>
export default {
  name: 'AppMain',

  props: {
    currentMonth: Number,
    currentYear: Number
  },

  data: () => ({
    days: ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su']
  }),

  methods: {
    getCurrentDay() {
      if (this.currentMonth === new Date().getMonth()
      && this.currentYear === new Date().getFullYear()) {
        return new Date().getDate()
      }
      return null
    }
  },

  computed: {
    currentDay() {
      return this.getCurrentDay()
    },

    startFrom() {
      const day = new Date(this.currentYear, this.currentMonth).getDay()
      return day === 0 ? 6 : day - 1
    },

    countOfDays() {
      return new Date(this.currentYear, this.currentMonth + 1, -1).getDate() + 1
    },
  }
}
</script>

<style lang="less" scoped>
.dayList {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-gap: 25px 20px;
  padding: 25px 10px;
  margin: 0;
}

.day {
  text-align: center;

  &:nth-child(7n),
  &:nth-child(7n - 1) {
    color: red;
  }
}

.today {
  border: 1px solid green;
}
</style>