<template>
  <div class="image">
      <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Youtube_loading_symbol_1_(wobbly).gif" alt="" v-if="loadingGif">
  </div>
  <div class="content">
    <p v-if="dogFact">{{ dogFact }}</p>
    <p v-else-if="errorMessage">{{ errorMessage }}</p>
    <p v-else><b>Loading...</b></p>
    <button @click="refresh">Yenile!</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dogFact: null,
      errorMessage: '',
      loadingGif: true
    }
  },
  async created() {
    await this.loadData();
  },
  methods: {
    async loadData() {
      try {
        await new Promise(resolve => setTimeout(resolve, 3000));
        const response = await fetch('https://dog-api.kinduff.com/api/facts');
        if(response.status === 200) {
          const data = await response.json();
          this.dogFact = data.facts[0];
          this.errorMessage = '';
        } else {
          this.errorMessage = `Sayfa yüklenirken bir hata oluştu: ${response.status} hata kodu`;
          console.log('API hatası', response.statusText);
        }
        this.loadingGif = false;
      }
      catch(error) {
        this.errorMessage = `Sayfa yüklenirken bir hata oluştu: ${error.message}`;
        console.log('API hatası', error.message);
      }
    },
    refresh() {
      this.loadingGif = true;
      this.dogFact = ''
      this.loadData();
    }
  }
}
</script>

 <style>
 p {
    align-items: center;
    justify-content: center;
    display: flex;
 }
 div .image {
  align-items: center;
  justify-content: center;
  display: flex;
 }
 img {
  border-radius: 30px;
  width: 150px;
  height: 150px;
 }
 </style>
