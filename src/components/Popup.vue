<template>
  <div class="popup">
    <div class="yearPopup" v-show="yearPopup">
      <span>Year:</span>
      <input type="number" :value="currentYear" @change="changeYear"/>
    </div>
    <ul class="monthsList" v-show="monthsPopup">
      <li class="month" 
        v-for="(month, index) in months" :key="`${ index }`"
        @click="$emit('changeCurrentMonth', index)"
      >
        {{ month }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Popup',

  props: {
    yearPopup: Boolean,
    monthsPopup: Boolean,
    months: Array,
    currentYear: Number
  },

  methods: {
    changeYear(e) {
      const year = Number(e.target.value)
      this.$emit('changeCurrentYear', year)
    }
  }
}
</script>

<style lang="scss" scoped>
.popup {
  position: absolute;
  top: 0;
  width: 100%;
  background: #ccc;
  border-radius: 0 0 10px 10px;
}

.yearPopup {
  text-align: center;
  padding-bottom: 20px;
}

input {
  width: 75px;
  background: rgba(0, 0, 0, 0);
  border-radius: 10px;
  border: 1px solid #000;
  text-align: center;
  margin-left: 10px;
  outline: none;

  &[type=number]::-webkit-inner-spin-button, 
  &[type=number]::-webkit-outer-spin-button { 
    -webkit-appearance: none; 
    margin: 0;
  }
}

.monthsList {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  padding: 0 0 10px;
  margin: 0;
}

.month {
  margin: auto;
  width: 30%;

  &:hover {
    text-decoration: underline;
  }
}
</style>