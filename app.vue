<template>
  <div>
    <p v-if="dogFact !== null"> {{ dogFact }}</p>
    <p v-else>{{ errorMessage }}</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dogFact: null,
      errorMessage: null
    }
  },
  async created() {
    try {
      const response = await fetch('https://dog-api.kinduff.com/api/facts')
      if(response.status === 200) {
        const data = await response.json()
        this.dogFact = data.facts[0]
      } else if(response.status >= 400){
        this.errorMessage = `Cannot load a dog fact: ${response.status} error`
        console.log('API hatası', response)
      }
    }
    catch(error) {
      this.errorMessage = error.message
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
