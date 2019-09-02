<template>
  <div id="app" 
    :style="{
      background: `url(${currentBackground})`, 
      opacity: opacity
    }">
    <div id="calendar">
      <header>
        <span class="btn" @click="previousMonth">&lt;</span>
        <span>{{ months[currentMonth].toUpperCase() }}</span>
        <span>{{ currentYear }}</span>
        <span class="btn" @click="nextMonth">&gt;</span>
      </header>
      <main>
        <ul>
          <li v-for="(day, index) in days" :key="`a${index}`">{{ day }}</li>
          <li v-for="(day, index) in startFrom" :key="`b${index}`"></li>
          <li v-for="(day, index) in countOfDays" :key="`c${index}`">{{ day }}</li>
        </ul>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data: () => ({
    currentMonth: new Date().getMonth(),
    currentYear: new Date().getFullYear(),

    days: ['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс'],

    months: [
      'январь',
      'февраль',
      'март',
      'апрель',
      'май',
      'июнь',
      'июль',
      'август',
      'сентябрь',
      'октябрь',
      'ноябрь',
      'декабрь'
    ],

    backgrounds: [
      require('./assets/winter.jpg'),
      require('./assets/spring.jpg'),
      require('./assets/summer.jpg'),
      require('./assets/autumn.jpg'),
      require('./assets/winter.jpg')
    ],
    
    opacity: 0
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

    preloadImg(url, onload) {
      let img = new Image()
      img.src = url

      if (onload) {
        img.onload = () => this.opacity = 1
      }
    }
  },

  computed: {
    startFrom() {
      let day = new Date(this.currentYear, this.currentMonth).getDay()
      return day === 0 ? 6 : day - 1
    },

    countOfDays() {
      return (
        new Date(this.currentYear, this.currentMonth + 1, -1).getDate() + 1
      )
    },

    currentBackground() {
      return (
        this.backgrounds[Math.floor((this.currentMonth+1)/3)]
      )
    }
  },

  created() {
    const backgrounds = this.backgrounds
    backgrounds.forEach(url => {
      this.preloadImg(url)
    })
    this.preloadImg(this.currentBackground, true)
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
}

#app {
  width: 100vw;
  min-height: -webkit-fill-available;
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
  border: 1px solid #000;
}

header {
  border-radius: 10px 10px 0 0;
  padding: 20px;
  text-align: center;
  background: rgba(200, 200, 200, 0.9);

  span {
    user-select: none;
    display: inline-block;
    width: 90px;
    text-align: center;

    &:nth-child(3) {
      text-align: right;
    }
  }
}

.btn {
  width: 40px;

  &:hover {
    transition: 0.3s;
    transform: scale(1.6);
  }
}

ul {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  grid-gap: 2vw;
  height: 400px;
  padding: 15px;

  li {
    text-align: center;

    &:nth-child(7n),
    &:nth-child(7n - 1) {
      color: red;
    }
  }
}
</style>