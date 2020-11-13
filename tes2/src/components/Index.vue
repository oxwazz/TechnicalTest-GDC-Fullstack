<template>
<div class="constainer mx-auto mt-5" style="width: 600px">
  <h3>> >Pencarian Info Team Sepakbola</h3>
  <hr>
  <input v-model="nilai" type="text" class="form-control" placeholder="masukkan nama team sepakbola" aria-label="masukkan nama team sepakbola" aria-describedby="basic-addon1" style="width: 600px">
  <br>
  <button @click="getData" class="btn btn-primary" style="width: 600px"> Cari Info Team</button>
  <hr>

  <p>Nama Team: <b>{{dataTeam.namaTeam}}</b></p>
  <p>Negara: <b>{{dataTeam.negara}}</b></p>
  <p>Nama Stadium: <b>{{dataTeam.namaSatium}}</b></p>
  <p>Website: <b>{{dataTeam.website}}</b></p>
</div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      nilai: '',
      dataTeam: {
        namaTeam: '',
        negara: '',
        namaStadium: '',
        website: ''
      }
    }
  },
  methods: {
    async getData() {
      try {
        const {data} = await axios.get(`https://www.thesportsdb.com/api/v1/json/1/searchteams.php?t=${this.nilai}`)
        console.log(data.teams == null)
        if (data.teams == null) {
          this.dataTeam.namaTeam = "Data tidak ditemukan"
          this.dataTeam.negara = "Data tidak ditemukan"
          this.dataTeam.namaSatium = "Data tidak ditemukan"
          this.dataTeam.website = "Data tidak ditemukan"
        } else {
          this.dataTeam.namaTeam = data.teams[0].strAlternate
          this.dataTeam.negara = data.teams[0].strCountry
          this.dataTeam.namaSatium = data.teams[0].strStadium
          this.dataTeam.website = data.teams[0].strWebsite
        }
      } catch (e) {
        console.log(e)
      }
    }
  }
}
</script>

<style>

</style>
