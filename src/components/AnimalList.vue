<template>
    <div>
        <form v-on:submit.prevent="onSubmit">
            <label>Type: </label>
            <input v-model="newAnimal.type" type="text" placeholder="Type"><br>
            <label>Name: </label>
            <input v-model="newAnimal.name" type="text" placeholder="Name"><br>
            <label>Date of birth: </label>
            <input v-model="newAnimal.birth" type="text" placeholder="Date of birth"><br>
            <button type="submit" @click="addAnimal">Add animal</button>
        </form>
        <table>
            <thead>
                <th>Type</th>
                <th>Name </th>
                <th>Date of birth</th>
            </thead>
            <tbody>
                 <tr v-for="(animal, key) in animals" :key="key">                      
                      <td>{{animal.type}}</td>                     
                      <td>{{animal.name}}</td>
                      <td>{{animal.birth? animal.birth : "Nepoznato"}}</td>
                      <td><button type="submit" @click="removeAnimal(animal)">Remove</button></td>
                      <td><button type="submit" @click="moveToTop(animal)">Move to top</button></td>
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
              {type: "Lion", name: "LionName", birth:""},
              {type: "Wolf", name: "WolfName", birth:""},
              {type: "Fox", name: "FoxName", birth: "22-08-2015"},
              {type: "Rabbit", name: "RabbitName", birth: "24-10-2015"},
              {type: "Bear", name: "BearName", birth: "22-09-2016"}
          ],
          newAnimal: {
              type:'',
              name:'',
              birth:''
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
              }
     }
   
}
</script>