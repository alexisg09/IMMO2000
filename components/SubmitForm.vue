<template>
  <!--    action="https://formspree.io/f/xwkybdvz"-->

  <form
    @submit.prevent="sendForm"
  >
    <CFlex>
      <CTagLabel>
        Your email:
        <CInput v-model="email"/>
      </CTagLabel>
      <label>
        Your message:
        <CTextarea v-model="message"></CTextarea>
      </label>
      <CButton margin="3"
               variant-color="green"
               type="submit"
      >Send
      </CButton>
    </CFlex>

  </form>
</template>

<script>

import {
  CTagLabel,
  CFlex,
  CTextarea,
  CButton,
  CInput
} from '@chakra-ui/vue'

export default {
  name: 'SubmitForm',
  components: {
    CTagLabel,
    CFlex,
    CTextarea,
    CButton,
    CInput
  },

  // prop: {
  //   email: string,
  //   message: string
  // },

  data () {
    return {
      email: '',
      message: ''
    }
  },

  methods: {
    async sendForm (e) {
      e.preventDefault()
      const currentObj = this

      const res = await fetch('https://formspree.io/f/xwkybdvz', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },

        body: JSON.stringify({
          email: this.email,
          message: this.message
        })
      }).then(function (response) {
        currentObj.output = response.data
      }).catch(function (error) {
        currentObj.output = error
      })
    }
  }
}

</script>

<style>

</style>
