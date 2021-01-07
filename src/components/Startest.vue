<template>
  <b-container class="starContainer">
    <b-row class="justify-content-center">
        <b-col cols="4">
            <div>
                <b-card border-variant="light" header="Rating" class="text-center">
                    <b-card-text><h1>{{rating}}</h1></b-card-text>
                    <v-rating v-model="rating" dense half-increments hover size="28" readonly></v-rating>
                    <v-btn icon>
                        <v-icon>mdi-message-text</v-icon>
                        <b-card-text>Comment : {{comment.length}}</b-card-text>
                    </v-btn>
                </b-card>
            </div>
        </b-col>
        <b-col cols="1" class="num">
            <p>5</p>
            <p>4</p>
            <p>3</p>
            <p>2</p>
            <p>1</p>
        </b-col>
        <b-col cols="4">
            <div>
                <b-row>
                    <b-col>
                        <b-progress :value="power5" variant="success" class="mb-3"></b-progress>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col>
                        <b-progress :value="power4" variant="success" class="mb-3"></b-progress>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col>
                        <b-progress :value="power3" variant="success" class="mb-3"></b-progress>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col>
                        <b-progress :value="power2" variant="success" class="mb-3"></b-progress>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col>
                        <b-progress :value="power1" variant="success" class="mb-3"></b-progress>
                    </b-col>
                </b-row>
            </div>
        </b-col>
    </b-row>
</b-container>
</template>

<script>
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
      rating: 0,
      comment: 0
    }
  },
  methods: {
    async onestar () {
      try {
        var { data } = await this.axios.post('https://oneconf-dev3.cloudns.asia/feedback/OneScore')
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
        var { data } = await this.axios.post('https://oneconf-dev3.cloudns.asia/feedback/TwoScore')
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
        var { data } = await this.axios.post('https://oneconf-dev3.cloudns.asia/feedback/ThreeScore')
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
        var { data } = await this.axios.post('https://oneconf-dev3.cloudns.asia/feedback/FourScore')
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
        var { data } = await this.axios.post('https://oneconf-dev3.cloudns.asia/feedback/FiveScore')
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
      this.axios.post('https://oneconf-dev3.cloudns.asia/feedback/Rating')
        .then(response => {
          var average = response.data.average
          this.rating = average
        })
    },
    async getComment () {
      try {
        var { data } = await this.axios.get('https://oneconf-dev3.cloudns.asia/feedback/Data')
        console.log(data.data)
        this.comment = data.data
      } catch (error) {
        console.log(error.message)
      }
    },
    total () {
      var totalstar = this.star1 + this.star2 + this.star3 + this.star4 + this.star5
      this.power1 = (this.star1 / totalstar) * 100
      this.power2 = (this.star2 / totalstar) * 100
      this.power3 = (this.star3 / totalstar) * 100
      this.power4 = (this.star4 / totalstar) * 100
      this.power5 = (this.star5 / totalstar) * 100
    }
  }
}
</script>

<style scoped>
.starContainer {
    border-bottom : 1px solid #e4e1e1;
    background-color: white;
}
/* .star {
    display: flex;
    justify-items: start;
    margin: 40px 0 0 180px;
} */
/* .comment {
    display: flex;
    margin: 55px 0 0 -20px;
} */
/* .rating {
    display: flex;
    margin: 20px 0 0 -20px;
} */
.chart {
  margin: 0 0 0 0;
  padding: 10px 0 0 0;
}
.num {
  padding: 20px 0 0 60px;
}
.col {
  padding: 12px 0 0 0;
}

</style>
