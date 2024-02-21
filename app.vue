<template>
  <div>
    <p v-if="dogFact !== null"> {{ dogFact }}</p>
    <p v-else-if="errorMessage">{{ errorMessage }}</p>
    <p v-else>Loading...</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dogFact: null,
      errorMessage: ''
    }
  },
  async created() {
    try {
      const response = await fetch('https://dog-api.kinduff.com/api/facts')
      if(response.status === 200) {
        const data = await response.json()
        this.dogFact = data.facts[0]
      } else {
        this.errorMessage = `Sayfa yüklenirken bir hata oluştu: ${response.status} hata kodu`
        console.log('API hatası', response.statusText)
      }
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
 </style>
