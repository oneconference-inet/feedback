<template>
  <b-container class="CommentContainer">
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
export default {
  name: 'Comment',
  created () {
    this.getData()
  },
  data () {
    return {
      rating: 5,
      items: [],
      items_page: [],
      page: 1,
      page_length: 1,
      roomname: 'name'
    }
  },
  computed: {
    numberOfPages () {
      return Math.ceil(this.page_length)
    }
  },
  methods: {
    async getData () {
      try {
        var { data } = await this.axios.get(
          process.env.VUE_APP_API + '/api/feedback/data'
        )
        // this.items = data.data
        // this.items_page = data.data
        this.items = data.data
        console.log('items', this.items)
        for (let i = 0; i < this.items.length; i++) {
          if (this.items[i].score === -1) {
            this.items[i].score = 0
          }
          if (this.items[i].message === '') {
            this.items[i].message = 'ไม่มีการแสดงความคิดเห็น'
          }
          if (this.items[i].room === '') {
            this.items[i].room = 'ไม่มีชื่อห้อง'
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
    },
    // async getRoom () {
    //   var room = await this.axios.post(
    //     "http://localhost:9213/api/Histoy_rooms/search",
    //     { meeting_id: this.test }
    //   )
    // }
  }
}
</script>

<style scoped>
.CommentContainer {
  background-color: white;
}
.DialogComment {
  display: flex;
  margin: 0 0 0 0;
}
/* .star {
    display: flex;
    margin: 0 0 0 330px;
} */
.comment {
  width: 100px;
  height: 200px;
}
</style>
