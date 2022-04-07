<template>
  <div class="container">
    <CBox
      v-bind="mainStyles[colorMode]"
      d="flex"
      w="100vw"
      h="100vh"
      flex-dir="column"
      justify-content="center"
    >
      <CIconButton
        mr="3"
        :icon="colorMode === 'light' ? 'moon' : 'sun'"
        :aria-label="`Switch to ${
              colorMode === 'light' ? 'dark' : 'light'
            } mode`"
        @click="toggleColorMode"
      />
      <CHeading text-align="center" mb="4">
        🏠 Bienvenue chez IMMO2000 🏠
      </CHeading>
      <CFlex justify="center" direction="column" align="center">
        <CBox mb="3">

          <CButton
            left-icon="info"
            variant-color="blue"
            @click="showToast"
          >
            Show Toast
          </CButton>
        </CBox>
        <CBox>
          <NuxtLink :to="'/bien_immo/' + data.id" v-for="data in datas" :key="data.id">
            <BienImmo v-if="data" :bien-immo="data"/>
          </NuxtLink>
        </CBox>
      </CFlex>
    </CBox>
  </div>
</template>

<script lang="js">
import {
  CBox,
  CButton,
  CIconButton,
  CFlex,
  CHeading
} from '@chakra-ui/vue'

import axios from 'axios'

export default {
  name: 'IndexPage',
  components: {
    CBox,
    CButton,
    CIconButton,
    CFlex,
    CHeading
  },
  inject: ['$chakraColorMode', '$toggleColorMode'],
  data () {
    return {
      showModal: false,
      mainStyles: {
        dark: {
          bg: 'gray.700',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'white',
          color: 'gray.900'
        }
      },
      datas: null,
    }
  },
  async mounted () {
    const { data } = await axios.get('http://localhost:1337/api/bien-immos')

    console.log(data)
    this.datas = data.data
  },
  computed: {
    colorMode () {
      return this.$chakraColorMode()
    },
    theme () {
      return this.$chakraTheme()
    },
    toggleColorMode () {
      return this.$toggleColorMode
    }
  },
  methods: {
    showToast () {
      this.$toast({
        title: 'Account created.',
        description: 'We\'ve created your account for you.',
        status: 'success',
        duration: 10000,
        isClosable: true
      })
    },

  }
}
</script>
