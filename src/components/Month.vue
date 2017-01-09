<template>
  <div class="month">
    <span v-on:click="back">back</span>
    <span v-on:click="forward">foward</span>
    <h2>{{ month.name }}, {{ year }}</h2>
    <div class="grid">
      <div class="header">
        <ul class="days-of-the-week">
          <li>Sunday</li>
          <li>Monday</li>
          <li>Tuesday</li>
          <li>Wednesday</li>
          <li>Thursday</li>
          <li>Friday</li>
          <li>Saturday</li>
        </ul>
      </div>
      <week v-for="week in weeks"
            v-bind:index="week.index"
            v-bind:sunday="week.sunday"></week>
    </div>
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
      if (this.index < 0) {
        this.index = 11
        this.year -= 1
      }
      this.update()
    },

    forward: function () {
      this.index += 1
      if (this.index > 11) {
        this.index = 0
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
          sunday: this.date.toString(),
          index: this.index
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
  margin: 0;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0;
  padding: 0;
}

a {
  color: #42b983;
}

.days-of-the-week {
  display: none;
}

@media (min-width: 700px) {
  .grid {
    width: 700px;
    margin: 0 auto;
  }

  .header {
    margin-bottom: 1em;
  }

  .days-of-the-week {
    display: table-row;
    height: 2em;
    background-color: #ccc;
  }
  .days-of-the-week > li {
    display: table-cell;
    width: 86px;
    padding-top: .5em;
  }
}

@media (min-width: 910px) {
  .grid {
    width: 910px;
  }
  .days-of-the-week > li {
    width: 130px;
  }
}

@media (min-width: 1190px) {
  .grid {
    width: 1190px;
  }
  .days-of-the-week > li {
    width: 170px;
  }
}

@media (min-width: 1505px) {
  .grid {
    width: 1505px;
  }
  .days-of-the-week > li {
    width: 215px;
  }
}
</style>
