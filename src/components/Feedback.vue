<template>
  <b-container class="starContainer">
    <b-row class="justify-content-center">
        <b-col cols="4" class="box">
            <div>
                <b-card border-variant="success" header="Rating" class="text-center">
                    <b-card-text><h1>{{rating1}}</h1></b-card-text>
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
    <b-row>
        <div>
      <div class="DialogComment" v-for="item in items" :key="item.id">
        <b-row>
          <b-col cols="3" class="star">
            <b-card>
              <h1 class="text-center">{{item.score}}</h1>
              <v-rating
                v-model="item.score"
                background-color="indigo lighten-3"
                color="indigo"
                readonly
              ></v-rating>
              <p class="text-center">Date : {{item.created_at}}</p>
            </b-card>
          </b-col>
          <b-col cols="9" class="comment">
            <b-card>
              <div class="overline">Room : {{item.room}}</div>
              <b-card-text>{{item.message}}</b-card-text>
            </b-card>
          </b-col>
        </b-row>
      </div>
    </div>
    </b-row>
        <v-container text-center>
          <div class="overline">Page {{ page }} of {{ numberOfPages }}</div>
      <v-btn fab dark color="blue darken-3" class="mr-3" @click="formerPage">
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <v-btn fab dark color="blue darken-3" class="ml-3" @click="nextPage">
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
    </v-container>
</b-container>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'

export default {
  name: 'Star',
  created () {
    this.onestar()
    this.twostar()
    this.threestar()
    this.fourstar()
    this.fivestar()
    this.getRating()
    this.getComment()
    this.getData()
  },
  components: {
    apexchart: VueApexCharts
  },
  data () {
    return {
      power1: 0,
      power2: 0,
      power3: 0,
      power4: 0,
      power5: 0,
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
      rating1: 0,
      comment: 0,
      items: [],
      items_page: [],
      page: 1,
      page_length: 1,
      allStar: [],
      chartOptions: {
        chart: {
          width: 380,
          type: 'pie'
        },
        labels: ['5 ดาว', '4 ดาว', '3 ดาว', '2 ดาว', '1 ดาว'],
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
        this.star2 = data.data
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
          this.rating1 = average
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
      this.allStar.push(this.star5, this.star4, this.star3, this.star2, this.star1)
    },
    async getData () {
      try {
        var { data } = await this.axios.get(
          process.env.VUE_APP_API + '/api/feedback/data'
        )
        // this.items = data.data
        // this.items_page = data.data
        this.items = data.data
        for (let i = 0; i < this.items.length; i++) {
          if (this.items[i].score === -1) {
            this.items[i].score = 0
          }
          if (this.items[i].message === '') {
            this.items[i].message = 'ไม่มีการแสดงความคิดเห็น'
          }
          if (this.items[i].room === '') {
            this.items[i].message = 'ไม่มีชื่อห้อง'
          }
        }
        this.items_page = data.data
      } catch (error) {
        console.log(error.message)
      }
      this.getPage()
    },
    getPage () {
      const number1 = (this.items_page.length / 4).toFixed(2)
      const number2 = number1 - parseInt(number1)
      if (number2 === 0) {
        this.page_length = parseInt(number1)
      } else {
        this.page_length = parseInt(number1) + 1
      }
      this.getDataPage()
    },
    getDataPage () {
      var item = []
      var numberAdd = this.page * 4
      for (let i = 0; i < numberAdd; i++) {
        if (this.items_page[i] !== undefined) {
          item.push(this.items_page[i])
        }
      }
      if (this.page !== 1) {
        var numberDelete = (this.page - 1) * 4
        for (let i = 0; i < numberDelete; i++) {
          item.shift(this.items_page[i])
        }
      }
      this.items = item
    },
    nextPage () {
      if (this.page + 1 <= this.numberOfPages) this.page += 1
      this.getDataPage()
    },
    formerPage () {
      if (this.page - 1 >= 1) this.page -= 1
      this.getDataPage()
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
