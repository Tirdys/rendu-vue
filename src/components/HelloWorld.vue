<template>
  <div>

  <!-- Add "scoped" attribute to limit CSS to this component only 
    <h1 id="text">Test</h1><br>
    <img id="imggg" style="width: 20%" src="http://assets.stickpng.com/thumbs/58482acecef1014c0b5e4a1e.png">
    </br></br><button v-on:click="logg">Log</button>
    <button v-on:click="disp">Disparaitre</button>
    <button v-on:click="appa">Apparaitre</button>
    <button v-on:click="imgg">Image</button> 

  -->

  <div class="block">
    <h2 id="titre"></h2>
<label>Ecrire un numéro de pokemon :</label>
<input type="text" id="inputt" name="name" required>
<button v-on:click="pokemon">Envoyer</button>
  </div>



<table>
  <tr>
    <td>Nom</td>
    <td>Type</td>
    <td>Image normal</td>
    <td>Image Shiny</td>
  </tr>
  <tr>
    <td><p id="test"></p></td>
    <td><label id="typepoke"></label></td>
    <td><img id="pokeimg2" src=""></img></td>
    <td><img id="pokeimg" src=""></img></td>
  </tr>
</table>



  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }, methods : { /* -------- CI DESSOUS LES EXERCICES 1 ET 2 (l'exercice 3 est fait avec le rendu final) --------
    logg : function (event) {
      console.log("press")
    },

    disp : function(event){
      text.style.display = "none";
    },

    appa : function(event){
      text.style.display = "block";
    },

     imgg : function(event){
     
     if(imggg.src != "https://www.lsa-conso.fr/mediatheque/6/8/0/000362086_5.jpg" ){

     imggg.src = "https://www.lsa-conso.fr/mediatheque/6/8/0/000362086_5.jpg"

     } else {
       imggg.src = "http://assets.stickpng.com/thumbs/58482acecef1014c0b5e4a1e.png"
     }
    } */

    pokemon : function(event){
      
      

      const idd = inputt.value
      const url = "https://pokeapi.co/api/v2/pokemon/" + idd

    if (idd >= 1 && idd <= 898) {
      titre.innerHTML = ""

      axios.get(url)
      .then(function (response) {
    console.log(response);
    test.innerHTML = response.data.name


    if (response.data.types.length != 1){
       
      typepoke.innerHTML = response.data.types[0].type.name + " et " + response.data.types[1].type.name
    } else {
      typepoke.innerHTML = response.data.types[0].type.name
    }

    

    

    pokeimg.src = response.data.sprites.front_shiny
    pokeimg2.src = response.data.sprites.front_default
    })

      
    } else {
      titre.innerHTML = "Une erreur est survenue, merci de mettre une valeur comprise entre 1 et 898"
    }

    },

  } 

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.block {
}

#test {
  font-weight: bold;
  color: blue;
}

label{
  font-weight: bold;
}

table {
  
  background-color: yellow;
   border-collapse: collapse;
  width : 90%;
  margin-top: 5%;
  margin-left: auto;
  margin-right: auto;
}

td{
  border: solid black 2px;
}

#titre{
  color : red;
}
</style>
