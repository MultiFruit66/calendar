<template>
  <div id="app" 
    :style="{
      background: `url(${ currentBackground })`, 
      opacity: opacity
    }">
    <div id="calendar">
      <appHeader 
        :months="months" 
        :currentMonth="currentMonth" 
        :currentYear="currentYear"
        @previousMonth="previousMonth"
        @openMonthsPopup="openMonthsPopup"
        @openYearPopup="openYearPopup"
        @nextMonth="nextMonth"
      />
      <main>
        <popup 
          :months="months"
          :monthsPopup="monthsPopup"
          :yearPopup="yearPopup"
          :currentYear="currentYear"
          @changeCurrentMonth="changeCurrentMonth"
          @changeCurrentYear="changeCurrentYear"
        />
        <appMain 
          :currentMonth="currentMonth" 
          :currentYear="currentYear"
        />
      </main>
    </div>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader'
import AppMain from './components/AppMain'
import Popup from './components/Popup'

export default {
  name: 'App',

  components: {
    AppHeader,
    AppMain,
    Popup
  },

  data: () => ({
    currentMonth: new Date().getMonth(),
    currentYear: new Date().getFullYear(),

    months: [
      'January', 'February', 'March', 'April',
      'May', 'June', 'July', 'August',
      'September', 'October', 'November', 'December'
    ],

    backgrounds: [
      require('./assets/winter.jpg'),
      require('./assets/spring.jpg'),
      require('./assets/summer.jpg'),
      require('./assets/autumn.jpg')
    ],
    
    opacity: 0,

    monthsPopup: false,
    yearPopup: false
  }),

  methods: {
    nextMonth() {
      this.currentMonth += 1

      if (this.currentMonth > 11) {
        this.currentMonth = 0
        this.currentYear += 1
      }
    },

    previousMonth() {
      this.currentMonth -= 1

      if (this.currentMonth < 0) {
        this.currentMonth = 11
        this.currentYear -= 1
      }
    },

    changeCurrentMonth(num) {
      this.currentMonth = num
      this.monthsPopup = false
    },

    changeCurrentYear(num) {
      this.currentYear = num
      this.yearPopup = false
    },

    openMonthsPopup() {
      this.monthsPopup = !this.monthsPopup
    },

    openYearPopup() {
      this.yearPopup = !this.yearPopup
    },

    preloadImg(url, onload) {
      const img = new Image()
      img.src = url

      if (onload) {
        img.onload = () => this.opacity = 1
      }
    }
  },

  computed: {
    currentBackground() {
      return this.backgrounds[Math.floor((this.currentMonth + 1) / 3) % 4]
    }
  },

  mounted() {
    this.preloadImg(this.currentBackground, true)

    const backgrounds = this.backgrounds
    backgrounds.forEach(url => this.preloadImg(url))

    window.addEventListener('keydown', event => {
      switch (event.keyCode) {
        case 37: this.previousMonth() 
          break
        case 38: this.currentYear += 1 
          break
        case 39: this.nextMonth() 
          break
        case 40: this.currentYear -= 1 
          break
      }
    })
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
}

#app {
  width: 100vw;
  height: -webkit-fill-available;
  min-height: 90vh;
  display: flex;
  font-size: 22px;
  transition: .7s;
  background-repeat: no-repeat;
  background-size: cover;
}

#calendar {
  margin: auto;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 10px;
  height: 450px;
  border: 1px solid #000;
  user-select: none;
  cursor: default;
}

main {
  position: relative;
}
</style>