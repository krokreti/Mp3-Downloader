<template>
  <div class="d-flex justify-content-center" id="bg-all">
    <div class="p-4 " id="bg-main">

    <h1 class="text-white display-4 text-center" style="font-family: Mabook; "> < Video > </h1>
    <h1 class="text-white display-6 text-center" style="font-family: Mabook; " ><em>para</em></h1>
    <h1 class="display-4 text-center"> <p style="font-family: Summer; color: #ab79d6; text-shadow: 2px 2px 10px #00bbcb;">MP3</p></h1>

    <div>
      <InputForm v-model="endereco" />
    </div>
    <div class="d-flex justify-content-end mb-2" >
      <ButtonForm :nomeBotao="'Buscar'" class="pr-4" @click="formatUrl()"/>
      <ButtonForm :nomeBotao="'Limpar'" :tipoBotao="'btn btn-outline-info'" class="pr-4" @click="limpar()" />
    </div>
      <TableFormVue :video="video" v-if="video" class="mt-4"/>
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
      this.video= "";
    },
    formatUrl() {
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

      axios.request(options).then(response => {
        console.log(response.data)
        this.video = response.data
      }).catch(function (error) {
        console.error(error);
      });
      // 13182e
    }

  },
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}


@font-face {
  font-family: Summer;
  src: url("../static/SummerSunshine.woff");
}

@font-face {
  font-family: Mabook;
  src: url("../static/Mabook.woff");
}

#bg-all {
  background-image: linear-gradient(to bottom right, #14162f, #13182e);
  height: max-content;
  width: 100%;
}

#bg-main {
  width: 100vw;
  background-image: url("../static/wallpaper.jpg");
  background-size: cover;
  background-attachment: fixed;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  overflow: auto;
}

@media (min-width:1200px) {
  #bg-main {    
    width: 30%;
    height: 100vh;
    background-size: 30% 100%;
    overflow: auto;
  }
  #bg-main::-webkit-scrollbar {
    display: none;
}
}

@media (min-width: 576px) { 

 }



</style>