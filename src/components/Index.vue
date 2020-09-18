<template>
  <b-container fluid="md" class="md">
    <div>
      <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark">
        <template v-slot:header>DPLK Glosarium </template>
        <template v-slot:lead>
         Istilah istilah yang ada di DPLK
        </template>
      </b-jumbotron>
    </div>
    <div class="mt-3">
      <b-button-group>
        <b-button class="btn">#</b-button>
        <b-button class="group">A</b-button>
      </b-button-group>
    </div>
    <b-row class="b-row-2">
      <b-input-group size="lg" class="col-md-12">
        <b-input-group-prepend is-text>
          <b-icon icon="search"/>
        </b-input-group-prepend>
        <b-form-input v-model="keyword" type="search" placeholder="Search terms" @keyup.enter="keyPressEvt"/>
      </b-input-group>
    </b-row>
    <b-row class="justify-content-md-center">
      <b-col>
      <b-list-group class="b-list" v-for="(v, $index) in data" :key="$index">
        <b-list-group-item>
          <h2>{{ v.title }}</h2>
          <p>{{ v.description }}</p>
        </b-list-group-item>
      </b-list-group>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import data from '../assets/data'

export default {
  name: 'Index',
  data () {
    return {
      keyword: '',
      data: data
    }
  },
  methods: {
    filterData (data, q) {
      if (q == null || q === '') return data
      return data.filter((v) => {
        return v.title.toLowerCase().includes(q.toLowerCase())
      })
    },
    keyPressEvt: function (event) {
      this.data = this.filterData(data, this.keyword)
    }
  }
}
</script>

<style scoped>
  .md {
    margin-top: 10px !important;
  }
  .b-list {
    margin-top: 20px !important;
  }
  .mt-3 {
    margin-top: 0px !important;
  }
  .b-row-2 {
    margin-top: 10px !important;
  }
  .group {
    margin-left: 10px !important;
  }
</style>
