<template>
  <div class="home">
    <img
      alt="Vue logo"
      src="../assets/logo.png"
    >
  </div>
</template>

<script>
// const API_URL = "https://api.mercadolibre.com/sites/MLA/search?q=ssd"

export default {
  data () {
    return {
      variable: 'hola',
      items: ['sdas']
    }
  },
  created () {

  },
  mounted () {
    console.log(this.variable)
    this.fetch()
  },
  methods: {
    fetch () {
      this.$axios.get("https://api.mercadolibre.com/sites/MLA/search?q=ssd")
        .then((response) => {
          // handle success
          this.items = response.data.results
          console.log(this.items)
        })
        .catch((error) => {
          // handle error
          console.log(error)
        })
        .then(() => {
          // always executed
        })
    }
  }
};
</script>

