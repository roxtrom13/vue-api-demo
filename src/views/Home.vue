// Todo esto de template es solo html
<template>
  <v-container>
    <h1>Busca tu película</h1>
    <v-divider></v-divider>
    <v-form>
      <v-container>
        <v-row>
          <v-col cols="8">
            <!-- Este es el campo de texto y recibiremos acá el id que se guarda en la variable movieID (línea 45) como string -->
            <v-text-field
              v-model="movieID"
              label="Ingresa el ID de una película"
            ></v-text-field>
            <!-- Este es el botón que va a ejecutar la función search (linea 52) que en realidad accionará axios para traer la data del API -->
            <v-btn color="success" @click="search">Buscar</v-btn>
          </v-col>
        </v-row>
        <v-row>
          <hr>
          <ul>
          <!-- acá hago un for con v-for en vez de un foreach, hago una iteración en names, cada elemento lo llamo name (eso es esa wea de "name in names") y lo de :key
          es un identificador único que es necesario para que vue no se confunda -->
            <li v-for="name in names" :key="name.id">
              <!-- acá usas doble llaves si quieres imprimir un dato javascript en html -->
              <!-- lo de first_name es el nombre que me da el api, revisas la consola para que entiendas -->
              name: {{name.first_name}} // last name: {{name.last_name}}
            </li>
          </ul>
        </v-row>
      </v-container>
    </v-form>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",

  // en esta sección se hacen las declaraciones de las variable que luego se usan arriba en la parte html(template)
  data() {
    return {
      // acá solo declaro las dos variables, el primero para el ID que usamos para el api y el segundo va a guardar lo respuesta
      movieID: "",
      names: [],
    };
  },
  methods: {

    // esta es la función que se acciona cuando hago click en el botón, mira la línea 16 en donde dice @click
    search() {

      // acá primero convierto el id que estaba en string(línea 45) a int porque así lo pide el api
      var page = parseInt(this.movieID); //cuando nos referimos a los datos de data(), hay que usar this.

      // luego paso ese id al final del url
      axios.get("https://reqres.in/api/users?page="+page).then((res) => {
        console.log(res.data.data);
        // acá guardo la respuesta en la variable que definí en data(), ve la línea 46
        this.names = res.data.data;
      });
    },
  },
};
</script>
