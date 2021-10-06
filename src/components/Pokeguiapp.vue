<template>
  <div id="App">
    <div class="search">
      <h1>Pokeguia</h1>
      <label for="pokemon">Escribe el nombre de tu pokemon :</label>
      <input
        type="text"
        name="pokemon"
        v-model="nombrePokemon"
        autofocus
        placeholder="pikachu"
      />
      <button @click="peticionApi">Buscar</button>
    </div>
    <section class="info">
      <h2>{{pokeNombre}}</h2>
      <img :src="pokeImg" alt />

      <div class="movesyAbilities">
        <div class="moves">
          <h3>Movimientos</h3>
          <ul>
            <li v-for="(move , i) in pokeMoves" :key="i">{{move.move.name}}</li>
          </ul>
        </div>

        <div class="abilities">
          <h3>habilidades</h3>
          <ul>
            <li v-for="(ability , i) in pokeAbilities" :key="i">{{ability.ability.name}}</li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "pokeguía",
  data() {
    return {
      nombrePokemon: "",
      pokemon: {
        name: "",
        sprites: {
          front_default: "",
        },
        moves: [],
        abilities: [],
      },
    };
  },
  // metodo para llamar a la api y entrar con pikachu al inicio
  methods: {
    peticionApi() {
      fetch(this.url)
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          this.pokemon = data;
          this.nombrePokemon = "";
        })
        .catch((error) => console.log(`Hubo un error: \n${error} intentalo de nuevo`));
    },
  },
  created() {
    this.peticionApi();
  },
  computed: {
    url() {
      return this.nombrePokemon.trim() == ""
        ? `https://pokeapi.co/api/v2/pokemon/pikachu`
        : `https://pokeapi.co/api/v2/pokemon/${this.nombrePokemon
            .toLowerCase()
            .trim()}`;
    },
    pokeNombre() {
      return this.pokemon.name.toUpperCase();
    },
    pokeImg() {
      return this.pokemon.sprites.front_default;
    },
    pokeMoves() {
      return this.pokemon.moves;
    },
    pokeAbilities() {
      return this.pokemon.abilities;
    },
  },
};
</script>

<style lang="scss">
* {
margin: 20px;
box-sizing: border-box;
}
#app {
font-family: Helvetica, sans-serif;
text-align: center;
min-height: 100vh;
background-color: rgb(255, 255, 255);
}
.search {
padding: 30px 0;

h1 {
    padding: 10px;
    font-size: 50px;
}
h5 {
    color: rgb(0, 0, 0);
}
}
.info {
 margin: 200px;
  img {
    width: 20%;
  }
  .movesyAbilities{
    display: flex;
    flex-direction: column;
    h3 {
      text-align: center;
      padding: 16px ;
      font-size: 30px;
    }
.moves{
      ul {
        columns: 6;
        font-size: 24px;
      }
    }
  }
}
ul {
  li {
    text-align: center;
    margin: 5 px , 5px;
  }
}

.abilities{
     ul {
        columns: 6;
        font-size: 24px;
      }
    } 


</style>