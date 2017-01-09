<template>
  <div class="week">
    <div>{{ sunday }}</div>
    <div v-for="day in days">
      <span>{{ day.name }}</span>
      <span>{{ day.date }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'week',
  props: ['sunday'],
  data () {
    return {
      days: [{
        name: 'Sunday',
        date: ''
      }, {
        name: 'Monday',
        date: ''
      }, {
        name: 'Tuesday',
        date: ''
      }, {
        name: 'Wednesday',
        date: ''
      }, {
        name: 'Thursday',
        date: ''
      }, {
        name: 'Friday',
        date: ''
      }, {
        name: 'Saturday',
        date: ''
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
      let date = new Date(this.sunday)
      this.days.map(function (day, index) {
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
</style>
