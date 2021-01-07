<template>
  <b-container class="CommetContainer">
    <div>
      <div class="DialogComment"  v-for="item in items" :key="item.id">
        <b-row>
          <b-col cols="3" class="star">
            <b-card>
              <h1 class="text-center">{{ item.score }}</h1>
              <v-rating
                v-model="item.score"
                background-color="indigo lighten-3"
                color="indigo"
                readonly
              ></v-rating>
              <p class="text-center">Date : {{ item.created_at }}</p>
            </b-card>
          </b-col>
          <b-col cols="9" class="comment">
            <b-card>
              <div class="overline">Room : {{ item.room }}</div>
              <b-card-text>
                {{ item.message }}
              </b-card-text>
            </b-card>
          </b-col>
        </b-row>
      </div>
    </div>
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
      items: [
      ],
      search: null
    }
  },
  computed: {
    filteredList () {
      console.log('filterlist')
      var text = this.search.trim()
      return this.items.filter(item => {
        return item.room.indexOf(text) > -1
      })
      // return this.items
    }
  },
  methods: {
    async getData () {
      try {
        var { data } = await this.axios.get('https://oneconf-dev3.cloudns.asia/feedback/Data')
        console.log(data.data)
        this.items = data.data
      } catch (error) {
        console.log(error.message)
      }
    }
  }
}
</script>

<style scoped>
.CommetContainer {
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
