<template>
  <div>
    <Header />

    <div style="padding:20px;"></div>
    <Encrypt />
    <div style="padding:20px;"></div>
    <Decrypt />
  </div>
</template>

<script>
  import Encrypt from '../components/Encrypt'
  import Header from '../components/Header'
  import Decrypt from '../components/Decrypt'

  export default {
    name: 'Home',

    components: {
      Encrypt,
      Header,
      Decrypt
    },
  }
</script>
