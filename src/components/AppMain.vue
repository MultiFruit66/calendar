<template>
  <ul class="dayList">
    <li class="day" v-for="(day, index) in days" :key="`c${ index }`">{{ day }}</li>
    <li class="day" v-for="(day, index) in startFrom" :key="`d${ index }`"></li>
    <li class="day" v-for="(day, index) in countOfDays" :key="`e${ index }`">{{ day }}</li>
  </ul>
</template>

<script>
export default {
  name: 'AppMain',

  props: {
    days: Array,
    startFrom: Number,
    countOfDays: Number
  }
}
</script>

<style lang="scss" scoped>
.dayList {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-gap: 25px 20px;
  padding: 25px 10px;
  margin: 0;

  .day {
    text-align: center;

    &:nth-child(7n),
    &:nth-child(7n - 1) {
      color: red;
    }
  }
}
</style>