<template>
  <div>
    <div class="container text-center " >
      <div class="row ">
        <div class="col d-flex align-items-center justify-content-center font-weight-bold border rounded bg-light ">
          Título: 
        </div>
        <div class="col border rounded bg-light">
          {{ video.title }}
        </div>
      </div>
      <div class="row">
        <div class="col d-flex align-items-center justify-content-center font-weight-bold border rounded bg-light">
          Canal:
        </div>
        <div class="col border rounded bg-light">
          {{ video.author }}
        </div>
      </div>
      <div class="row">
        <div class="col d-flex align-items-center justify-content-center font-weight-bold border rounded bg-light">
          Duração:
        </div>
        <div class="col border rounded bg-light">
          {{ video.length }}
        </div>
      </div>
      <div class="row border d-flex align-items-center justify-content-center rounded bg-light  p-2">
        <img :src="video.thumb" alt="Thumb" class="border rounded-lg ">
      </div>
    </div>
          <div class="mt-2">
        <a :href="linkDownload" target="_blank">
            <ButtonForm :nomeBotao="'Baixar'" :tipoBotao="'btn btn-success w-100'"/>
        </a>
      </div>
  </div>
</template>

<script>
import axios from "axios";
import ButtonForm from './ButtonForm.vue';

export default {
    name: 'TableForm',
    props: {
        video: null,
    },
    data() {
        return {
            linkDownload: null,
            qualidade: [],
        }
    },
    components: {
      ButtonForm,
      
    },
    created() {
        this.baixar(this.video.id)
    },
    methods: {
        async baixar(id) {
            const options = {
            method: 'GET',
            url: 'https://youtube-mp3-download1.p.rapidapi.com/dl',
            params: {id},
            headers: {
                'X-RapidAPI-Key': 'd0146d5790msh6ba282319190f7cp1e8e7cjsn56997398e517',
                'X-RapidAPI-Host': 'youtube-mp3-download1.p.rapidapi.com'
            }
            };

            axios.request(options).then( response => {
                this.linkDownload = response.data.link
                console.log('response link: ')
                console.log(response.data);
            }).catch(function (error) {
                console.error(error);
            });
        }
    },
}
</script>

<style>

</style>