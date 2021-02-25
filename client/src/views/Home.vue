<template>
  <v-app>
    <!-- Must have the app property -->
    <v-app-bar app></v-app-bar>

    <v-main>
      Hello World
    </v-main>
  </v-app>
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
          this.calcular()
        })
    },
    calcular () {
      this.items.forEach(element => {
        console.log(element.price)
      })
      this.items.sort((a, b) => (a.price < b.price) ? 1 : -1)
      console.log(this.items)
    }
  },
};
</script>

