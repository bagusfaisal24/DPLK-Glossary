<template>
  <b-container class="md">
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
        <b-button @click="keyPressEvt">#</b-button>
      </b-button-group>
      <b-button-group v-for="(v, $index) in abjad" :key="$index">
        <b-button class="btn" @click="onClick(v)">{{ v }}</b-button>
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
      data: data,
      abjad: []
    }
  },
  mounted () {
    this.abjad = this.groupping(data)
  },
  methods: {
    filterData (data, q) {
      if (q == null || q === '') return data
      return data.filter((v) => {
        return v.title.toLowerCase().includes(q.toLowerCase())
      })
    },
    filterIndexChart (data, q) {
      if (q == null || q === '') return data
      return data.filter((v) => {
        return v.title.charAt(0).toLowerCase().includes(q.toLowerCase())
      })
    },
    groupping (data) {
      const newArr = []
      data.filter((v) => {
        if (newArr.indexOf(v.title.charAt(0)) === -1) {
          newArr.push(v.title.charAt(0))
        }
      })
      return newArr
    },
    keyPressEvt: function (event) {
      this.data = this.filterData(data, this.keyword)
    },
    onClick: function (event) {
      console.log(event)
      this.data = this.filterIndexChart(data, event)
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
  .btn {
    margin-left: 10px !important;
  }
</style>
