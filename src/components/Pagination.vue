<template>
  <b-container class="bg">
    <div>
      <b-row>
        <b-col cols="2">
        </b-col>
        <b-col cols="2">
        </b-col>
        <b-col cols="8">
          <div class="mt-3">
            <b-pagination v-model="currentPage" :total-rows="rows" align="right"></b-pagination>
          </div>
        </b-col>
      </b-row>
    </div>
  </b-container>
</template>

<script>
export default {
  name: 'Pagination',
  data () {
    return {
      value1: 5,
      rows: 100,
      currentPage: 1
    }
  }
}
</script>

<style scoped>
.bg {
    background-color: white;
}
</style>
