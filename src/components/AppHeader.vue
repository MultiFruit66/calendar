<template>
  <header>
    <span class="btn" @click="$emit('previousMonth')">&lt;</span>
    <span class="data" @click="$emit('openMonthsPopup')">{{ months[currentMonth] }}</span>
    <span class="data" @click="$emit('openYearPopup')">{{ currentYear }}</span>
    <span class="btn" @click="$emit('nextMonth')">&gt;</span>
  </header>
</template>

<script>
export default {
  name: "AppHeader",

  props: {
    months: Array, 
    currentMonth: Number, 
    currentYear: Number
  }
}
</script>

<style lang="scss" scoped>
header {
  border-radius: 10px 10px 0 0;
  padding: 20px;
  text-align: center;
  background: rgba(200, 200, 200, 0.9);
  white-space: nowrap;
}

.data, .btn {
  display: inline-block;
  transition: .3s;
}

.data {
  width: 100px;
  text-align: center;

  &:hover {
    text-decoration: underline;
  }

  &:nth-child(3) {
    width: 60px;
  }
}

.btn {
  width: 40px;

  &:hover {
    transform: scale(1.6);
  }
}
</style>