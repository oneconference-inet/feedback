<template>
  <b-container class="starContainer">
    <b-row class="justify-content-center">
        <b-col cols="4" class="box">
            <div>
                <b-card border-variant="success" header="Rating" class="text-center">
                    <b-card-text><h1>{{rating}}</h1></b-card-text>
                    <v-rating v-model="rating" dense half-increments hover size="28" readonly></v-rating>
                    <v-btn icon>
                        <v-icon>mdi-message-text</v-icon>
                        <b-card-text>Comment : {{comment.length}}</b-card-text>
                    </v-btn>
                </b-card>
            </div>
        </b-col>
        <b-col cols="4">
            <div id="chart">
                <apexchart type="pie" width="380" :options="chartOptions" :series="allStar"></apexchart>
            </div>
        </b-col>
    </b-row>
</b-container>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'

export default {
  name: 'Star',
  created () {
    this.nostar()
    this.onestar()
    this.twostar()
    this.threestar()
    this.fourstar()
    this.fivestar()
    this.getRating()
    this.getComment()
  },
  components: {
    apexchart: VueApexCharts
  },
  data () {
    return {
      star0: [
      ],
      star1: [
      ],
      star2: [
      ],
      star3: [
      ],
      star4: [
      ],
      star5: [
      ],
      rating: 0,
      comment: 0,
      allStar: [],
      chartOptions: {
        chart: {
          width: 380,
          type: 'pie'
        },
        labels: ['5 ดาว', '4 ดาว', '3 ดาว', '2 ดาว', '1 ดาว', 'ไม่ให้ดาว'],
        colors: ['#6DD66D', '#46CCFF', '#A0A0FF', '#14A0A0', '#DB7A9D', '#bebebe'],
        responsive: [{
          breakpoint: 480,
          options: {
            chart: {
              width: 200
            },
            legend: {
              position: 'bottom'
            }
          }
        }]
      }
    }
  },
  methods: {
    async nostar () {
      try {
        var { data } = await this.axios.post(
          process.env.VUE_APP_API + '/api/feedback/NoScore'
        )
        // console.log(data.data)
        // this.star0 = data.data
        if (data.data !== 'NoData') {
          this.star0 = data.data.length
        } else {
          this.star0 = 0
        }
      } catch (error) {
        console.log(error.message)
      }
    },
    async onestar () {
      try {
        var { data } = await this.axios.post(
          process.env.VUE_APP_API + '/api/feedback/OneScore'
        )
        // console.log(data.data)
        // this.star1 = data.data
        if (data.data !== 'NoData') {
          this.star1 = data.data.length
        } else {
          this.star1 = 0
        }
      } catch (error) {
        console.log(error.message)
      }
    },
    async twostar () {
      try {
        var { data } = await this.axios.post(
          process.env.VUE_APP_API + '/api/feedback/TwoScore'
        )
        // console.log(data.data)
        // this.star2 = data.data
        if (data.data !== 'NoData') {
          this.star2 = data.data.length
        } else {
          this.star2 = 0
        }
      } catch (error) {
        console.log(error.message)
      }
    },
    async threestar () {
      try {
        var { data } = await this.axios.post(
          process.env.VUE_APP_API + '/api/feedback/ThreeScore'
        )
        // console.log(data.data)
        // this.star3 = data.data
        if (data.data !== 'NoData') {
          this.star3 = data.data.length
        } else {
          this.star3 = 0
        }
      } catch (error) {
        console.log(error.message)
      }
    },
    async fourstar () {
      try {
        var { data } = await this.axios.post(
          process.env.VUE_APP_API + '/api/feedback/FourScore'
        )
        // console.log(data.data)
        // this.star4 = data.data
        if (data.data !== 'NoData') {
          this.star4 = data.data.length
        } else {
          this.star4 = 0
        }
      } catch (error) {
        console.log(error.message)
      }
    },
    async fivestar () {
      try {
        var { data } = await this.axios.post(
          process.env.VUE_APP_API + '/api/feedback/FiveScore'
        )
        // console.log(data.data)
        // this.star5 = data.data
        if (data.data !== 'NoData') {
          this.star5 = data.data.length
        } else {
          this.star5 = 0
        }
        this.total()
      } catch (error) {
        console.log(error.message)
      }
    },
    getRating () {
      this.axios.post(
        process.env.VUE_APP_API + '/api/feedback/Rating'
      )
        .then(response => {
          var average = response.data.average
          this.rating = average
        })
    },
    async getComment () {
      try {
        var { data } = await this.axios.get(
          process.env.VUE_APP_API + '/api/feedback/data'
        )
        console.log(data.data)
        this.comment = data.data
      } catch (error) {
        console.log(error.message)
      }
    },
    total () {
      this.allStar.push(this.star5, this.star4, this.star3, this.star2, this.star1, this.star0)
    }
  }
}
</script>

<style scoped>
.starContainer {
    border-bottom : 1px solid #e4e1e1;
    background-color: white;
}
.box {
  margin: 0 30px 0 0;
  padding: 40px 0 0 0;
}
/* .num {
  padding: 20px 0 0 60px;
} */
/* .col {
  padding: 12px 0 0 0;
} */

</style>
