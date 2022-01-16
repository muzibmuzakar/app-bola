<template>
  <div class="container">
    <router-link to="/" class="btn btn-primary btn-sm">Create Club</router-link>
    <div class="table-club">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">First</th>
            <th scope="col">Last</th>
            <th scope="col">Handle</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(club, index) in clubs.data" :key="index">
            <th scope="row">1</th>
            <td>{{ club.name }}</td>
            <td>{{ club.homebase }}</td>
            <td><img :src="url+club.image" style="width:100px;"></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import {onMounted, ref} from 'vue'

export default{
  setup() {
    let url = 'http://localhost:8000/storage/images/clubs/'
    let clubs = ref([]);

    onMounted(() => {
      axios.get('http://localhost:8000/api/club')
      .then((result) => {
        clubs.value = result.data
      }).catch((err) => {
        console.log(err)
      });
    });

    return {
      clubs,
      url
    }
  },
}
</script>

