<template>
  <v-container>
    <v-text-field
      label="Buscar Articulo de MercadoLibre"
      placeholder="Ej. Descarrilador Shimano"
      filled
      v-model="busquedaInput"
      @keydown.enter="buscarML"
    >
      <v-icon slot="append">
        mdi-shopping-search
      </v-icon>
    </v-text-field>
    <span>Mostrar articulo con:</span>
    <v-chip>Mas ventas </v-chip>
    <v-chip>asdasd</v-chip>
    <v-chip>asdasd</v-chip>
    <v-data-table
      :loading="loadingMainTabla"
      loading-text="Cargando... Espere"
      multi-sort
      :headers="headers"
      :items="items"
      :items-per-page="10"
      class="elevation-1"
    >
      <template v-slot:item.price="{ item }">
        $ {{ item.price}}
      </template>
      <template v-slot:item.links="{ item }">
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-icon
              @click="abrirPestania(item.permalink)"
              v-bind="attrs"
              v-on="on"
            >
              mdi-link-variant
            </v-icon>
          </template>
          <span>Ir al articulo</span>
        </v-tooltip>
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-icon
              @click="abrirPestania(item.thumbnail)"
              v-bind="attrs"
              v-on="on"
            >
              mdi-image
            </v-icon>
          </template>
          <span>Ver imagen</span>
        </v-tooltip>
        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-icon
              @click="abrirPestania(item.seller.permalink)"
              v-bind="attrs"
              v-on="on"
            >
              mdi-account-circle
            </v-icon>
          </template>
          <span>Pagina del vendedor</span>
        </v-tooltip>

      </template>
      <!-- <template v-slot:item.seller.permalink="{ item }">
        <a :href="item.seller.permalink">
          {{ item.seller.pernalink }}
        </a>
      </template> -->
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      busquedaInput: "",
      headers: [
        {
          text: "ID MLA",
          align: "start",
          sortable: false,
          value: "id",
        },
        { text: "Articulo", value: "title" },
        { text: "Precio", value: "price" },
        { text: "Links", value: "links", sortable: false },
      ],
      items: [],
      loadingMainTabla: false,
    };
  },
  created () { },
  mounted () { },
  methods: {
    buscarML () {
      this.loadingMainTabla = true;
      this.$axios
        .get(
          "https://api.mercadolibre.com/sites/MLA/search?q=" +
          encodeURIComponent(this.busquedaInput)
        )
        .then((response) => {
          // handle success
          this.items = response.data.results;
          console.log(this.items);
          this.loadingMainTabla = false;
        })
        .catch((error) => {
          // handle error
          console.log(error);
        })
        .then(() => {
          // always executed
        });
    },
    abrirPestania (link) {
      window.open(link, "_blank");
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
