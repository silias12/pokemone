<html><head> 
  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script> 
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous"> 
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script> 
 </head> 
 <body> 
  <div id="app1" class="container"> 
   <h1 class="text-primary"> {{titulo}} </h1>
  <div class="row">
      <div class="col-sm">
  <ul>
    <li v-for="poke in pokemones">
        <button v-on:click="verPoke(poke.url,poke.name)" class="btn btn-link">{{poke.name}} </button>
    </li>        
  </ul>
  </div>
  <div class="col-sm"> Imagen del pokemon
      <br>
      <img v-bind:src="imgPoke">
      <br>
      <h3 class="text-danger">{{nombrePoke}}</h3>
      </div>
      </div>
      <div class="row">
          <div class="col-sm">
      <button v-on:click="pidePokes(siguiente)" class="btn btn-primary">
          Siguientes pokemones</button>
  Total de Pokemones: {{total}}
  <button v-on:click="pidePokes(anterior)" class="btn btn-warning">
      Anteriores pokemones</button>
  </div> 
</div></div>
    <script>
     var app=new Vue({ 
        el:"#app1", 
        data: 
        {   
                    titulo:"API de Pokemones", 
                    url:"http://pokeapi.co/api/v2/pokemon", 
                    total: 0, 
                    siguiente: "", 
                    anterior: "", 
                    pokemones:[], 
                    pokemon:[], 
                    nombrePoke: "", 
                    imgPoke:"", 
        }, 
        mounted(){ 
                    this.pidePokes(this.url); 
                    this.verPoke("https://pokeapi.co/api/v2/pokemon","bulbasaur"); 
          }, 
        methods: 
        {     
                    pidePokes: async function(url) 
                    { 
                    const response = await fetch(url); 
                    this.pokemones = await response.json(); 
                    this.total = this.pokemones.count; 
                    this.siguiente = this.pokemones.next; 
                    this.anterior = this.pokemones.previous; 
                    this.pokemones = this.pokemones.results; 
                     }, 
            verPoke:async function(urlPoke,nombrePoke) 
             { 
                 const response=await fetch(urlPoke); 
                 this.pokemon=await response.json(); 
                 this.pokemon=this.pokemon.sprites.other 
                 this.nombrePoke=nombrePoke; 
                 this.imgPoke=this.pokemon.dream_world.front_default; 
             } 
                        
        }, 
                     
})
  </script>
    </body></html>
