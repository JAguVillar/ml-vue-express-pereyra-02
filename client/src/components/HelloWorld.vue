<template>
  <v-container>
    <v-data-table
      loading
      multi-sort
      dense
      :headers="headers"
      :items="items"
      :items-per-page="5"
      class="elevation-1"
    >
      <template v-slot:item.permalink="{ item }">
        <a :href="item.permalink">
          {{ item.permalink }}
        </a>
      </template>
      <template v-slot:item.thumbnail="{ item }">
        <a :href="item.thumbnail">
          {{ item.thumbnail }}
        </a>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      variable: 'hola',
      headers: [
        {
          text: 'ID MLA',
          align: 'start',
          sortable: false,
          value: 'id',
        },
        { text: 'Articulo', value: 'title' },
        { text: 'Precio', value: 'price' },
        { text: 'Link', value: 'permalink' },
        { text: 'Imagen', value: 'thumbnail' },
        { text: 'Vendedor', value: 'seller.permalink' },
      ],
      items: [],
      loading: true
    }
  },
  created () {
  },
  mounted () {
    this.fetch()
  },
  methods: {
    fetch () {
      this.$axios.get("https://api.mercadolibre.com/sites/MLA/search?q=ssd")
        .then((response) => {
          // handle success
          this.items = response.data.results
          console.log(this.items)
          this.loading = false
        })
        .catch((error) => {
          // handle error
          console.log(error)
        })
        .then(() => {
          // always executed
        })
    },
    // calcular () {
    //   this.items.forEach(element => {
    //     console.log(element.price)
    //   })
    //   this.items.sort((a, b) => (a.price < b.price) ? 1 : -1)
    //   console.log(this.items)
    // }
  },
};
</script>


