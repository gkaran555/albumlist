<template>
  <v-container fluid grid-list-md>
    <infinite-slide-bar :barStyle="{ background: '#fff7cc', padding: '5px 0' }">
      <span style="color: #f60;">Click on one of the Albums</span>
    </infinite-slide-bar>
    <v-data-iterator
      :items="albums"
      :rows-per-page-items="pagination.rowsPerPageItems"
      :pagination.sync="pagination"
      content-tag="v-layout"
      row
      wrap
    >
    
      <v-flex slot="item" slot-scope="props" xs12 sm6 md4 lg3>
        <div class="home-album" @click="goToImg(props.item.id)">         
          <p class="home-text">{{props.item.title}} </p>
        </div>
      </v-flex>
    </v-data-iterator>

     <!-- <div class="home">
    <div class="home-album" v-for="album in albums" :key="album.id" @click="goToImg(album.id)">         
      <p class="home-text">{{album.title}} </p>
    </div>
    </div> -->

  </v-container>
  
</template>

<script>
import axios from 'axios'
import InfiniteSlideBar from 'vue-infinite-slide-bar'

export default {
    name: 'home',
    components: {
        InfiniteSlideBar
    },
    data() {
      return {
          albums: [],
          pagination: {
            rowsPerPageItems: [10, 20, 30],
            rowsPerPage: 10
          }
      };
    },

    methods: {
      fetchBreeds(){
        axios.get('https://jsonplaceholder.typicode.com/albums')
        .then((response)=> this.albums = response.data)
        .catch((error) => this.errors = error.response.data.errors)
      },
      goToImg(albumId) {
        this.$router.push(`/about/${albumId}`);
      }
    },
    mounted(){
      this.fetchBreeds();
    }

}
</script>


<style lang="scss" scoped>

img {
  width: 100%;
}
.home-album {
  height: 120px;
  box-shadow: 0 1px 2px 0 rgba(0,0,0,.5);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
    &:hover p {
    color: #c0963c;
    transition: 0.7s;
  }
  .home-text {
    font-size: 1rem;
    font-weight: 300;
    color: #838383;
    text-transform: uppercase;
  }
}
.vifnslb-container {
  position: absolute;
  top: 0px;
  left: 0px;
  right: 0px;
}

</style>