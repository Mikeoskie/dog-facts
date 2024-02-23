<template>
  <div v-if="loading" class="loading">
    <div class="image">
      <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Youtube_loading_symbol_1_(wobbly).gif" alt="">
    </div>
    <p><b>Loading...</b></p>
  </div>
  <div v-else>
    <p v-if="errorMessage">{{ errorMessage }}</p>
    <p v-else>{{ dogFact }}</p>
    <button @click="refresh">Yenile!</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dogFact: null,
      errorMessage: '',
      loading: true
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
          console.log('API hatası1', response.statusText);
        }
      }
      catch(error) {
        this.errorMessage = `Sayfa yüklenirken bir hata oluştu: ${error.message}`;
        console.log('API hatası2', error.message);
      }
      this.loading = false
    },
    refresh() {
      this.loading = true;
      this.dogFact = ''
      this.loadData();
    }
  }
}
</script>

 <style>
 p, b {
    align-items: center;
    justify-content: center;
 }
 div .loading {
  align-items: center;
  justify-content: center;
  text-align: center;
 }
 img {
  border-radius: 30px;
  width: 150px;
  height: 150px;
 }
 </style>
