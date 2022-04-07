<template>
  <div v-if="data">hello {{ data.id }}</div>

</template>

<script>

import axios from 'axios'

export default {

  data: function () {
    return {
      data: null,
    }
  },
  async mounted () {
    const { data } = await axios.get('http://localhost:1337/api/bien-immos/' + this.$route.params.id)

    this.data = data.data
    console.log(this.data)

  },
}


</script>
