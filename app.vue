<template>
  <div>
    <div class="image">
      <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Youtube_loading_symbol_1_(wobbly).gif" alt="" v-if="loadingGif">
    </div>
    <p v-if="dogFact !== null"> {{ dogFact }}</p>
    <p v-else-if="errorMessage">{{ errorMessage }}</p>
    <p v-else><b>Loading...</b></p>
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
    try {
      await new Promise (resolve => setTimeout(resolve, 3000))
      const response = await fetch('https://dog-api.kinduff.com/api/facts')
      if(response.status === 200) {
        const data = await response.json()
        this.dogFact = data.facts[0]
      } else {
        this.errorMessage = `Sayfa yüklenirken bir hata oluştu: ${response.status} hata kodu`
        console.log('API hatası', response.statusText)
      }
      this.loadingGif = false
    }
    catch(error) {
      this.errorMessage = `Sayfa yüklenirken bir hata oluştu: ${response.status} hata kodu`
      console.log('API hatası', error.message)
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
