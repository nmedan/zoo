<template>
    <div>
        <form v-on:submit.prevent>
            <label>Type: </label>
            <input v-model="newAnimal.type" type="text" placeholder="Type"><br>
            <label>Name: </label>
            <input v-model="newAnimal.name" type="text" placeholder="Name"><br>
            <label>Date of birth: </label>
            <input v-model="newAnimal.birth" type="text" placeholder="Date of birth"><br>
            <label>Sector:</label>
            <select v-model="newAnimal.sector">
                <option v-for="(sector, key) in sectors" :key="key" v-bind:value="sector">
                    {{sector.name}}
                </option>
            </select><br>
            <button type="submit" @click="addAnimal">Add animal</button>
        </form>
        <h2>Animals</h2>
        <table>
            <thead>
                <th>Type</th>
                <th>Name </th>
                <th>Sector </th>
                <th>Date of birth</th>
            </thead>
            <tbody>
                 <tr v-for="(animal, key) in animals" :key="key" v-bind:style="animal.background? styleBackground : ''">                      
                      <td>{{animal.type}}</td>                     
                      <td>{{animal.name}}</td>
                      <td>{{animal.sector.name}}</td>
                      <td>{{animal.birth? animal.birth : "Nepoznato"}}</td>
                      <td><button type="submit" @click="removeAnimal(animal)">Remove</button></td>
                      <td><button type="submit" @click="moveToTop(animal)">Move to top</button></td>
                 </tr>
            </tbody>
        </table>
        <h2>Sectors</h2>
        <table>
            <thead>
                <th>Name </th>

            </thead>
            <tbody>
                 <tr v-for="(sector, key) in sectors" :key="key">                      
                      <td>{{sector.name}}</td>                     
                      <td><button type="submit" @click="showAnimals(sector)">Show animals</button></td>
                 </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
  name: 'AnimalList',
  data() {
      return {
          animals:[
              {type: "Lion", name: "LionName", birth:"", sector:{}, background:true},
              {type: "Wolf", name: "WolfName", birth:"", sector:{}, background:false},
              {type: "Fox", name: "FoxName", birth: "22-08-2015", sector:{}, background:false},
              {type: "Rabbit", name: "RabbitName", birth: "24-10-2015", sector:{}, background:false},
              {type: "Bear", name: "BearName", birth: "22-09-2016", sector:{}, background:true}
          ],
          sectors:[
              {name:"Sector1"},
              {name:"Sector2"},
              {name:"Sector3"},
              {name:"Sector4"},
              {name:"Sector5"}              
          ],
          
          newAnimal: {
              
          },
          
          styleBackground: {
               background:'lightgreen',
          }
      };
    },
    methods: {
              addAnimal() {
                  console.log(this.newAnimal);
                  this.animals.push(this.newAnimal);
                  this.newAnimal = {};
              },

              removeAnimal(animal) {
                  let indexOfAnimalToRemove = this.animals.indexOf(animal);
                  this.animals.splice(indexOfAnimalToRemove, 1);
              },

              moveToTop(animal) {
                  let indexOfAnimalToRemove = this.animals.indexOf(animal);     
                  this.animals.splice(indexOfAnimalToRemove, 1);
                  this.animals.unshift(animal);           
              },

              showAnimals(sector) {
                  var i;
                  var animalsOfSector = [];
                  for(i=0; i<this.animals.length; i++) {
                      if (sector.name === this.animals[i].sector.name) {
                        animalsOfSector.push(this.animals[i].type + " " + this.animals[i].name);
                      }
                  }
                  alert(animalsOfSector.join('\n'));
              }
     }
   
}
</script>