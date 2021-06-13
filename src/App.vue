<template>
  <div id="app">
    <div id="progress">
      Ultimate Progress Bar 
    </div>
    <progress-bar title="Año" :total="year.total" :progress="year.progress" />
    <progress-bar title="Mes" :total="month.total" :progress="month.progress" />
    <progress-bar title="Semana" :total="week.total" :progress="week.progress" />
    <progress-bar title="Dia" :total="day.total" :progress="day.progress" />
    <progress-bar title="Hora" :total="hour.total" :progress="hour.progress" />
    <progress-bar title="Minuto" :total="minute.total" :progress="minute.progress" />
  </div>
</template>

<script>
import ProgressBar from './components/ProgressBar.vue'

export default {
  name: 'App',
  components: {
    ProgressBar
  },
  data() {
    return {
      year : {
        progress : 0,
        total : 0
      },
      month : {
        progress : 0,
        total : 0
      },
      week : {
        progress : 0,
        total : 7
      },
      day : {
        progress : 0,
        total : 24
      },
      hour : {
        progress : 0,
        total : 60
      },
      minute : {
        progress : 0,
        total : 60
      }
    }
  },
  mounted() {
    this.getParams()

    setInterval((context) => {
      context.getParams()
    }, 1000,this);
  },
  methods: {
    getDaysInMonth (year,month) {
      return new Date(year, month, 0).getDate();
    },
    getParams(){
      const now = new Date()    
      const start_date = new Date(now.getUTCFullYear(), 0, 0)    
      const daysOfYear = now.getFullYear() % 4 == 0 ? 366 : 365
      this.year.total = daysOfYear
      this.year.progress = Math.floor((now - start_date) / (1000 * 60 * 60 * 24))
      this.month.total = this.getDaysInMonth(now.getFullYear(),now.getMonth()+1)
      this.month.progress = now.getDate()
      this.week.progress = now.getDay()+1
      this.day.progress = now.getHours()
      this.hour.progress = now.getMinutes()
      this.minute.progress = now.getSeconds()
    }
  },
}

</script>

<style lang='sass'>
*
  margin: 0
  padding: 0
  box-sizing: border-box


#app 
  background: linear-gradient(.9turn,#5362ff,#ee4e4e)
  height: 100vh
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
  padding: 20px


#progress
  font-size: 30px
  font-family: Arial
  color: white
  letter-spacing: 25px
  text-align: center

</style>
