<template>
  <CBox>
    <CHeading text-align="center" mb="4">
      🏠 IMMO2000 🏠
    </CHeading>
    <CHeading>
      {{ bienImmo.attributes.city }}

    </CHeading>
    <h2>{{ bienImmo.attributes.livingSurface }} mètres carrés</h2>
    <h2 v-if="bienImmo.attributes.isToRent">A louer</h2>
    <h2 v-if="bienImmo.attributes.isToSell">A vendre</h2>

  </CBox>

</template>

<script>
export default {
  name: 'BienImmo',
  props: ['bienImmo'],
  mounted () {
    console.log(this.bienImmo)
  }
}


</script>

<style scoped>

</style>
