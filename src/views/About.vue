<template>
 <v-container fluid grid-list-md>
   <v-btn outline color="indigo"><router-link to="/">&#8592; Back to Albums</router-link></v-btn>
    <v-data-iterator
      :items="breedimg"
      :rows-per-page-items="pagination.rowsPerPageItems"
      :pagination.sync="pagination"
      content-tag="v-layout"
      row
      wrap
    >
      <v-flex slot="item" slot-scope="props" xs12 sm6 md4 lg3>
        <div v-if="props.item.albumId = albumId" @click="dialogopen(props.item)" class="album-box">
          <div class="album-img">
            <img :src="props.item.thumbnailUrl" alt="avatar">
          </div>
          <div class="album-content">
            <p class="album-title">{{ props.item.title }}</p>
          </div>
        </div>
      </v-flex>
    </v-data-iterator>

     <v-dialog v-model="dialog" max-width="290">
        <v-card>
          <v-img :src="reportimage.thumbnailUrl" height="200px">
          </v-img>
          <v-card-title primary-title>
            <div>
              <div class="headline">{{reportimage.title}}</div>
              <span class="grey--text">Album number {{albumId}}</span>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn color="green darken-1" flat="flat" @click="dialog = false">
               Close
            </v-btn>
          </v-card-actions>
        </v-card>  
     </v-dialog>

 </v-container>
</template>

<script>
import axios from 'axios'

export default {
    name: 'about',
    props: ['albumId'],
   
    data() {
      return {
          breedimg: [],
          pagination: {
            rowsPerPageItems: [10, 20, 30],
             rowsPerPage: 10
           },
          dialog: false,
          reportimage: [],
          show: false
      };
    },

    methods: {
      fetchImage(){
        axios.get('https://jsonplaceholder.typicode.com/photos')
        .then((response)=> this.breedimg = response.data)
        .catch((error) => this.errors = error.response.data.errors)
      },
      dialogopen: function(some) {
        this.dialog = true
        this.reportimage = some;
      }
    },
    mounted(){
      this.fetchImage();
    }
}
</script>


<style lang="scss" scoped>

.album-box {
  height: 70px;
  padding: 7px;
  box-shadow: 0 1px 2px 0 rgba(0,0,0,.5);
  display: flex;
  cursor: pointer;
  .album-img {
    flex: 0 0 25%;
    margin-right: 10px;
  }
  .album-content {
    text-align: left;
    .album-title {
      white-space: nowrap; 
      max-width: 20ch;
      overflow: hidden;
      text-overflow: ellipsis; 
      text-transform: uppercase;
  }
  }
}
.headline {
  text-transform: capitalize;
}
img {
  width: 100%;
  height: 100%;
}
a {
  text-decoration: none;
}


</style>
