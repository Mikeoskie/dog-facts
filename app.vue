<template>
  <div>
    <p> {{ dogFact }}</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dogFact: ''
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
