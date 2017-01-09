<template>
  <div class="week">
    <div style="display:none">{{ sunday }}</div>
    <div class="day"
         v-bind:class="{ inactive: !day.active }"
         v-for="day in days">
      <span>{{ day.name }}</span>
      <span>{{ day.date }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'week',
  props: ['sunday', 'index'],
  data () {
    return {
      days: [{
        name: 'Sunday',
        date: '',
        active: true
      }, {
        name: 'Monday',
        date: '',
        active: true
      }, {
        name: 'Tuesday',
        date: '',
        active: true
      }, {
        name: 'Wednesday',
        date: '',
        active: true
      }, {
        name: 'Thursday',
        date: '',
        active: true
      }, {
        name: 'Friday',
        date: '',
        active: true
      }, {
        name: 'Saturday',
        date: '',
        active: true
      }]
    }
  },
  created: function () {
    this.update()
  },

  beforeUpdate: function () {
    this.update()
  },

  methods: {
    update: function () {
      let that = this
      let date = new Date(this.sunday)
      this.days.map(function (day, index) {
        day.active = (date.getMonth() === that.index)
        day['date'] = date.toString()
        date.setDate(date.getDate() + 1)
      })
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

.day {
  background: #fff;
  border-top: 1px solid #ccc;
  border-left: 1px solid #ccc;
  border-right: 1px solid #ccc;
  box-sizing: border-box;
  padding-top: 1em;
  display: block;
  height: 7em;
  margin: 0;
  vertical-align: top;
  width: 100%;
}

.day:last-child {
  border-right: 1px solid #ccc;
}

.inactive {
  display:none;
}

@media (min-width: 700px) {
  .week {
    // border-top: 1px solid #ccc;
    width: 700px;
  }
  .week:last-child {
    border-bottom: 1px solid #ccc;
  }
  .day {
    border-right: 0;
    display: table-cell;
    height: 7em;
    vertical-align: top;
    width: 86px;
  }

  .inactive {
    background: #ddd;
    border-left: 1px solid #bbb;
  }
    
}

@media (min-width: 910px) {
  .week {
    width: 910px;
  }
  .day {
    width: 130px;
  }
}

@media (min-width: 1190px) {
  .week {
    width: 1190px;
  }
  .day {
    width: 170px;
  }
}

@media (min-width: 1505px) {
  .week {
    width: 1505px;
  }
  .day {
    width: 215px;
  }
}

</style>
