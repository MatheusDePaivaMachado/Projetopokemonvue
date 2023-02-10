<!-- eslint-disable no-unused-vars -->

  <template>
    <header class="header">
      <label class="caixadetexto" for="">
        Digite o nome do Pokémon:
        <input type="text" placeholder="Ex: pikachu..." v-model="pokemonID"> 
        <button class="searchButton" 
         @click="buscaPokemon">
        Pegue seu Pokémon</button>
      </label>
    </header>

      <main class="main"
        v-if="Object.entries(pokemonData).length > 0">
         <section class="pokemonCard">
            <div class="nameImage">
            <h2 class="pokemonName">{{ pokemonData.name }}</h2>
            <img class="img" :src="pokemonData.sprites.front_default" :alt="pokemonData.name">
            </div>
          <ul class="stats">
            <h3>Stats:</h3>
           <li 
             v-for="(stat, index) in pokemonData.stats" :key="index">
              <span>{{ stat.stat.name }} -- {{ stat.base_stat }}</span>
           </li>
         </ul>
        </section>
     </main>
  </template>

<script>
    // eslint-disable-next-line no-unused-vars
  import { pokeapi } from "@/api/pokeapi";

  export default{
  name: 'App',

  data() {
    return {
      pokemonData: {},
      pokemonID: '',
  }
  },

  methods: {
    async buscaPokemon () {
      try {
        const pokemonToFind = await fetch(`${pokeapi}/${this.pokemonID}`)
        const pokemon = await pokemonToFind.json()
          this.pokemonData = pokemon
            console.log(pokemon)
            return pokemon
      } catch (error) {
         alert('Ops! Pokémon não encontrado, tente novamente...')
      }
    }
  }
}
 





</script>

<style scoped>
  
.header {
  display: flex;
  justify-content: center;
  text-align: center;
  align-items: center;
  height: 50px;
  background-color:rgb(240, 179, 12);
  color: white;
  border-radius: 18px;
}

.header, input[type="text"], .searchButton {
  font-size: 18px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}


.main {
  font-size: 1.2rem;
  background-color:rgba(245, 242, 236, 0.884);  
  bottom: 40%;
  border-radius: 18px;
 
  }

 .caixadetexto {
  color: rgb(0, 0, 0);
  border-radius: 20px;
  cursor: pointer;
 }


.searchButton {
  background-color: #d1b96b;
  color: rgb(10, 9, 9);
  margin-left: 10px;
  border-radius: 18px;
  cursor: pointer;
  }

  .nameImage, .stats {
    width: 90%;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-direction: column;
   
  }
  .nameImage .pokemonName  {
      text-transform: capitalize;
      text-transform: uppercase;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      font-size: 18px;
    }

    
  

.pokemonCard {
  display: float-left;
  flex-direction: row;
  justify-content: space-around;
  align-content: center;
  border-radius:20px ;
  
  }


  .img {
      width: 200px;
      height: 200px;
      border-radius: 20%;
      
    
    }

  .stats    {
    position: absolute;
    border-radius: 18px;
    align-items: center;
    margin-left:-10px;
    background-color:rgba(245, 242, 236, 0.884);  
    width: 96.7%;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  

  .stats li  {
    align-self: flex-start;
    text-decoration: none;
    text-transform: uppercase;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 18px;
    margin-left: 42%;
    font-size: 1.2rem;
    background-color:rgba(245, 242, 236, 0.884);  
    bottom: 40%;
    border-radius: 18px;
    text-decoration: none;
    list-style: none;
  }

</style>
