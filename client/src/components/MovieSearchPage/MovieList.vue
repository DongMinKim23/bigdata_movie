<template>
  <v-container class="pa-2" fluid grid-list-md>
    <v-layout column>
      <v-flex v-for="card in movie_list" :key="card.id" pa-2>
        <MovieListCard
          :id="card.id"
          :img="card.img"
          :title="card.title"
          :genres="card.genres"
          :rating="card.rating"
          :view-cnt="card.viewCnt"
          :slug="card.slug"
          :poster="card.poster"
          :runtime="card.runtime"
          :director="card.director"
          :writer="card.writer"
          :actor="card.actor"
          :plot="card.plot"
          :country="card.country"
        />
      </v-flex>
      <v-pagination :total-visible="10" v-if="max_page > 1" v-model="page" :length="max_page" />
    </v-layout>
  </v-container>
</template>

<script>
import { mapState } from 'vuex';
import MovieListCard from './MovieListCard'

export default {
  components:{
    MovieListCard,
  },
  props:{
    movieListCards: {
      type: Array,
      default: () => new Array(),
    }
  },
  data(){
    return{
      page:0,
    }
  },
  computed: {
    ...mapState(['max_page','movie_list','filter'])
  },
  watch: {
    page(){
      this.$store.dispatch('SEARCH_MOVIES',this.filter+`&page=${this.page}`)
    }
  }
}
</script>
