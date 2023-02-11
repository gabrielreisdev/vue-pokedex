<template>
  <body>
    <main>
      <img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon__number}.png`"
        class="pokemon__image"
      />
      <h1 class="pokemon__data">
        <span class="pokemon__number">{{ pokemonData.id }}</span>
        -
        <span class="pokemon__name">{{ pokemonData.name }}</span>
      </h1>

      <form class="form">
        <input
          type="search"
          class="input__search"
          placeholder="Nome ou Número"
          required
          v-model="pokemon__number"
        />
        <button @click="searchPokemon" class="buttonSearch">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="14"
            height="14"
            fill="currentColor"
            class="bi bi-search"
            viewBox="0 0 16 16"
          >
            <path
              d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
            />
          </svg>
        </button>
      </form>

      <div class="buttons">
        <button class="button btn-prev">&lt; Anterior</button>
        <button class="button btn-next">Próximo &gt;</button>
      </div>
      <img src="./assets/pokedex.png" alt="pokedex" class="pokedex" />
    </main>

    <span class="main2">
      <img src="./assets/stats.png" class="stats" />

      <ul>
        <h2 class="pokemon__type">Tipo:</h2>
        <li v-for="(type, key) in pokemonData.types" :key="key">
          <span>{{ type.type.name }}</span>
        </li>
      </ul>

      <ul>
        <h2 class="pokemon__stats">Stats:</h2>
        <li v-for="(stat, key) in pokemonData.stats" :key="key">
          <span>{{ stat.stat.name }} -> {{ stat.base_stat }}</span>
        </li>
      </ul>

    </span>
  </body>
</template>

<script>
import { pokeapi } from "./api/api";

export default {
  name: "App",
  data() {
    return {
      pokemonData: {},
      pokemon__number: "",
    };
  },

  methods: {
    async searchPokemon() {
      try {
        const input__search = await fetch(`${pokeapi}/${this.pokemon__number}`);
        const pokemon = await input__search.json();
        this.pokemonData = pokemon;
        console.log(pokemon);
        return pokemon;
      } catch (error) {
        alert("Este pokemon não foi encontrado");
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Oxanium:wght@300;400;500;600;700;800&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Oxanium", cursive;
}

body {
  text-align: center;
  background: linear-gradient(to bottom, #3da4e9, #fff);
  min-height: fit-content;
}

main {
  display: inline-block;
  margin-top: 2%;
  position: relative;
}
.main2 {
  display: inline-block;
  margin-top: 2%;
  position: relative;
}

.pokedex {
  width: 100%;
  max-width: 350px;
}
.stats {
  width: 100%;
  max-width: 600px;
  height: 525px;
  position: relative;
}

.pokemon__image {
  position: absolute;
  bottom: 53%;
  left: 50%;
  transform: translate(-63%, 20%);
  height: 18%;
}
.pokemon__data {
  position: absolute;
  font-weight: 600;
  color: #aaa;
  top: 54.5%;
  right: 27%;
  font-size: clamp(8px, 5vw, 25px);
}

.pokemon__type {
  position: absolute;
  font-weight: 600;
  color: #aaa;
  top: 25%;
  right: 70%;
  font-size: clamp(8px, 5vw, 20px);
}

.pokemon__type li {
  position: absolute;
  font-weight: 600;
  color: #fff;
  top: 30%;
  right: 70%;
  font-size: clamp(8px, 5vw, 14px);
  display: inline-block;
}
.pokemon__stats {
  position: absolute;
  font-weight: 600;
  color: #aaa;
  font-size: clamp(8px, 5vw, 20px);
  right: 70%;
  top: 55%;
}
.pokemon__stats li {
  position: absolute;
  font-weight: 600;
  color: #fff;
  font-size: clamp(8px, 5vw, 14px);
  top: 60%;
  right: 70%;
  display: inline-block;
}

.pokemon__name {
  color: #3a444d;
  text-transform: capitalize;
}

.form {
  position: absolute;
  width: 65%;
  top: 65%;
  left: 13.5%;
}

.input__search {
  width: 100%;
  padding: 4%;
  outline: none;
  border: 2px solid #333;
  border-radius: 5px;
  font-weight: 600;
  color: #3a444d;
  font-size: clamp(8px, 5vw, 1rem);
  box-shadow: -3px 4px 0 #888, -5px 7px 0 #333;
}

.buttons {
  position: absolute;
  bottom: 10%;
  left: 50%;
  width: 65%;
  transform: translate(-57%, 0);
  display: flex;
  gap: 20px;
}

.button {
  width: 50%;
  padding: 4%;
  border: 2px solid #000;
  border-radius: 5px;
  font-size: clamp(5px, 5vw, 0.8rem);
  font-weight: 600;
  color: white;
  background-color: #444;
  box-shadow: -2px 3px 0 #222, -4px 6px 0 #000;
  height: 35px;
}
.buttonSearch {
  width: 15%;
  height: 33px;
  padding: 4%;
  border: 2px solid #000;
  border-radius: 5px;
  font-size: clamp(5px, 5vw, 1rem);
  font-weight: 600;
  color: white;
  background-color: #444;
  box-shadow: -2px 3px 0 #222, -4px 6px 0 #000;
  margin-top: 15px;
}
.buttonSearch svg {
  margin: auto;
}

.buttonSearch:active {
  box-shadow: inset -4px 4px 0 #222;
  font-size: 0.9rem;
}

.button:active {
  box-shadow: inset -4px 4px 0 #222;
  font-size: 0.7rem;
}
</style>
