<template>
  <div class="container">
    <router-link to="/" class="btn btn-primary btn-sm">Create player</router-link>
    <div class="table-player">
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
          <tr v-for="(player, index) in players.data" :key="index">
            <th scope="row">1</th>
            <td>{{ player.name }}</td>
            <td>{{ player.position }}</td>
            <td><img :src="url+player.photo" style="width:100px;"></td>
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
    let url = 'http://localhost:8000/storage/images/players/'
    let players = ref([]);

    onMounted(() => {
      axios.get('http://localhost:8000/api/player')
      .then((result) => {
        players.value = result.data
      }).catch((err) => {
        console.log(err)
      });
    });

    return {
      players,
      url
    }
  },
}
</script>