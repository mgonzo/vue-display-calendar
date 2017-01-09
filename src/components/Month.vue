<template>
  <div class="month">
    <span v-on:click="back">back</span>
    <span v-on:click="forward">foward</span>
    <h2>{{ month.name }}</h2>
    <week v-for="week in weeks"
          v-bind:sunday="week.sunday"></week>
  </div>
</template>

<script>
import Week from './Week'
export default {
  name: 'month',
  date: '',
  data () {
    return {
      index: '',
      month: '',
      year: '',
      weeks: [],
      months: [{
        name: 'January',
        days: 31
      }, {
        name: 'February',
        days: 28
      }, {
        name: 'March',
        days: 31
      }, {
        name: 'April',
        days: 30
      }, {
        name: 'May',
        days: 31
      }, {
        name: 'June',
        days: 30
      }, {
        name: 'July',
        days: 31
      }, {
        name: 'August',
        days: 31
      }, {
        name: 'September',
        days: 30
      }, {
        name: 'October',
        days: 31
      }, {
        name: 'November',
        days: 30
      }, {
        name: 'December',
        days: 31
      }]
    }
  },
  created: function () {
    this.date = new Date()
    this.index = this.date.getMonth()
    this.year = this.date.getFullYear()
    this.update()
  },

  components: {
    Week
  },

  methods: {
    back: function () {
      this.index -= 1
      if (this.index < 1) {
        this.index = 11
        this.year -= 1
      }
      this.update()
    },

    forward: function () {
      this.index += 1
      if (this.index > 11) {
        this.index = 1
        this.year += 1
      }
      this.update()
    },

    update: function () {
      this.reset()

      // set date to the first sunday
      let offset = this.date.getDay()
      this.date.setDate(this.date.getDate() - offset)

      // zero out the weeks
      this.weeks = this.weeks.slice(0, 0)

      // create weeks
      let i = 0
      while (i < (offset + this.months[this.index].days) / 7) {
        this.weeks.push({
          sunday: this.date.toString()
        })
        i += 1
        this.date.setDate(this.date.getDate() + 7)
      }

      // this.reset()
    },

    reset: function () {
      // reset the active date object
      this.date.setFullYear(this.year)
      this.date.setMonth(this.index)
      this.date.setDate(1)
      this.month = this.months[this.index]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0;
}

a {
  color: #42b983;
}
</style>
