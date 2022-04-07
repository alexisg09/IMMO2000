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
        🏠 Bien Immo 🏠
      </CHeading>
      <CFlex justify="center" direction="column" align="center">
        <CBox mb="3">
          <BienImmo/>
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
      datas: [],
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
      }
    }
  },
  async mounted () {
    const response = await axios.get('http://localhost:1337/api/bien-immos')
    this.data().datas = response
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
    getBienImmos () {

    }
  }
}
</script>
