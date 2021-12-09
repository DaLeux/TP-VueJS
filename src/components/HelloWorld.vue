<template>
  <div id="hello">
    <img src="https://logo-marque.com/wp-content/uploads/2020/05/Pokemon-Symbole.jpg" id="logo"/>
    <!--<button v-on:click="showe = !showe">Show</button>
    <transition name="fade">
      <p v-if="showe">bonjour</p>
    </transition>-->
    <p/>
    <input type="text" v-on:change="recherchepk">
    <table id="table">
      <tr>
        <th>Nom</th>
        <th>Standard</th>
        <th>Shiny</th>
        <th>Types</th>
        <th>Poids</th>
      </tr>
      <tr>
        <td>{{this.namePk}}</td>
        <td><img id="imgPkNormal"/></td>
        <td><img id="imgPkShiny"/></td>
        <td><p>{{this.typePk}}</p></td>
        <td>{{this.weightPk}}</td>
      </tr>  
    </table> 
    <!--<p>{{this.namePk}}</p>
    <p>{{this.weightPk}}</p>
    <img id="imgPkNormal"/>
    <img id="imgPkShiny"/>
    <p>{{this.typePk}}</p>-->
    
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      showe: true,
      namePk: '',
      spritePk: '',
      weightPk: '',
      typePk: '',
      lengthType: 0
    }
  },
  methods :{
    show: function(event) {
      console.log("press"),
      console.log(response)
    },
    recherchepk: function(event) {
      var url = "https://pokeapi.co/api/v2/pokemon/" + event.target.value
      //console.log(url)
      axios.get(url).then(response => {this.info = response.data
      //console.log(this.info.data['name']) // 

      this.namePk = this.info.name
      this.weightPk = this.info.weight + 'kg'
      document.getElementById('imgPkNormal').src = this.info.sprites.front_default
      document.getElementById('imgPkShiny').src = this.info.sprites.front_shiny
      //console.log(this.info)
      //console.log(this.info.types)


      this.lengthType = this.info.types.length
      for(let i = 0; i < this.info.types.length; i++) {
          //console.log(this.info.types[i].type.name)
          this.typePk = this.info.types[0].type.name

          if (i > 0) {
            this.typePk = this.typePk + ', ' + this.info.types[i].type.name
          }
          
      }
      console.log(this.typePk)
      
      //console.log(this.lengthType)
      })

      /*
        Element à afficher
        name = this.info.data['name']
        sprite = this.info.data['sprites']['front_default']
        weight = this.info.data['weight']
        types = for(let i == 0, i < this.info.data.types.length, i++) {
          
        }

      */
    }
  },
  mounted () {
    axios
      .get('https://pokeapi.co/api/v2/pokemon/1')
      .then(response => (this.info = response))
  }

}
</script>




<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#poketitle{
  color: yellow;
  border-color: blue;
}
#hello{
  height: 500px;
  background-color: #ffcc01;
}
#logo{
  height: 200px;
}
#table{
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
  width: auto;
}
</style>
