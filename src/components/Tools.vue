<template>
  <b-container class="bg">
    <div>
      <b-row>
        <!-- <b-col cols="2">
          <b-form inline>
            <b-input type="text" v-model="search"
              id="inline-form-input-name"
              class="mb-2 mr-sm-2 mb-sm-0"
              placeholder="Search room"
            ></b-input>
          </b-form>
        </b-col> -->
        <b-col cols="8">
          <!-- <div>
            <b-pagination v-model="currentPage" :total-rows="rows" align="right"></b-pagination>
          </div> -->
        </b-col>
      </b-row>
    </div>
    <Comment ref="searchValue"></Comment>
  </b-container>
</template>

<script>
import Comment from './Comment'
export default {
  name: 'Tools',
  components: {
    Comment
    // TestInput
  },
  data () {
    return {
      states: [
        'a', 'b', 'c', 'v'
      ],
      value1: 5,
      rows: 100,
      currentPage: 1,
      selectValue: null,
      commentInput: '',
      search: null
    }
  },
  watch: {
    search: {
      handler (value) {
        console.log('watch')
        this.$refs.searchValue.search = value
        console.log('dataRef', this.$refs.searchValue.search)
      },
      immediate: true
    }
  },
  computed: {
    filteredList () {
      return this.states.filter(post => {
        return post.title.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  },
  methods: {
    filterstates () {
      this.filterstates = this.state.filter(states => {
        return this.state.toLowerCase().startsWith(this.state.toLowerCase())
      })
    }
  }
}
</script>

<style scoped>
.bg {
  background-color: white;
}
</style>
