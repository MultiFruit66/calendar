<template>
  <div class="popup">
    <div class="yearPopup" v-show="yearPopup">
      <span>Year:</span>
      <input type="number" min="0" step="1" 
        :value="currentYear"
        @change="changeYear"
      />
    </div>
    <ul class="monthsList" v-show="monthsPopup">
      <li class="month" 
        v-for="(month, index) in months" :key="`a${ index }`"
        :ref="`month:${index}`"
        @click="changeMonth"
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
    changeMonth(e) {
      this.months.forEach((month, index) => {
        if (month === e.target.innerText) {
          this.$emit('changeCurrentMonth', index)
        }
      })
    },

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
  padding: 0 0 10px 10px;
}

input {
  width: 75px;
  background: rgba(0, 0, 0, 0);
  border-radius: 10px;
  border: 1px solid #000;
  text-align: center;
  margin-left: 10px;
}

.monthsList {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  padding: 0;
  margin: 0;
}

.month {
  margin: auto;
  width: 90px;

  &:hover {
    text-decoration: underline;
  }
}
</style>