<template>
  <div>
    <p v-if="dogFact !== null"> {{ dogFact }}</p>
    <p v-else>Cannot load a dog fact</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dogFact: null
    }
  },
  async created() {
    try {
      const response = await fetch('https://dog-api.kinduff.com/api/facts')
      const data = await response.json()
      if(response.status === 200) {
        this.dogFact = data.facts[0]
      } else {
        console.log('API hatası', response.statusText)
      }
    }
    catch(error) {
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
