<template>
  <div class="d-flex justify-content-center" id="bg-all">
    <div class="p-4 " id="bg-main">

    <h1 class="text-white display-4 text-center">Video</h1>
    <h1 class="text-white display-6 text-center"><em>para</em></h1>
    <h1 class="text-white display-4 text-center">MP3</h1>
    <div>
      <InputForm v-model="endereco" />
    </div>
    <div class="d-flex justify-content-end mb-2" >
      <ButtonForm :nomeBotao="'Buscar'" class="pr-4" @click="formatUrl()"/>
      <ButtonForm :nomeBotao="'Limpar'" :tipoBotao="'btn btn-outline-info'" class="pr-4" @click="limpar()" />
    </div>
    <TableFormVue :video="video" v-if="video"/>
    </div>
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
#bg-all {
  background-image: linear-gradient(to bottom right, #14162f, #13182e);
}

#bg-main {
  background-image: url("../static/wallpaper.jpg");
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  width: 100%;
  height: 100vh;
  
}

@media (min-width: 576px) { 
  #bg-main {
    width: 25%;
    height: 100vh;
    background-size: cover;
    background-size: 25% 100%;
    
    
  }
 }

</style>