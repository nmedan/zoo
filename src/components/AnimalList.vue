<template>
    <div>
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
          ]
          
      };
    },
    methods: {
        
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