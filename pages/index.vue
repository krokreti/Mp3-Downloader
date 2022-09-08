<template>
  <div class="p-4">
    <div>Video para MP3</div>
    <div>
      <InputForm v-model="endereco"/>
    </div>
    <div class="d-flex justify-content-end mb-2" >
      <ButtonForm :nomeBotao="'Buscar'" class="pr-4" @click="formatUrl()"/>
      <ButtonForm :nomeBotao="'Limpar'" :tipoBotao="'btn btn-outline-info'" class="pr-4" @click="limpar()" />
    </div>
    <TableFormVue :video="video" v-if="video"/>
  </div>
</template>

<script>
import axios from "axios";
import ButtonForm from '../components/Ui/ButtonForm.vue'
import InputForm from '../components/Ui/InputForm.vue'
import TableFormVue from '../components/Ui/TableForm.vue';

export default {
  data() {
    return {
      endereco: null,
      id: null,
      video : null,
    }
  },
  components: {
    InputForm,
    ButtonForm,
    TableFormVue,
  },
  methods: {
    limpar() {
      this.endereco = "";
    },
    formatUrl() {
      //https://www.youtube.com/watch?v=z5-3BiXsv0s&ab_channel=TalksCortes
      let arrayEndereco = this.endereco.split("https://www.youtube.com/watch?v=")
      let arraySplit = arrayEndereco[1].split("&")
      this.id = arraySplit[0]
      this.converter(this.id)
    },

    converter(id) {
      const options = {
        method: 'GET',
        url: 'https://youtube-video-download-info.p.rapidapi.com/dl',
        params: {id},
        headers: {
          'X-RapidAPI-Key': 'd0146d5790msh6ba282319190f7cp1e8e7cjsn56997398e517',
          'X-RapidAPI-Host': 'youtube-video-download-info.p.rapidapi.com'
        }
      };

      // axios.request(options).then(function (response) {
      //   console.log(response.data);
      axios.request(options).then(response => {
        console.log(response.data)
        this.video = response.data
      }).catch(function (error) {
        console.error(error);
      });
    }

  },
}
</script>

<style>

</style>