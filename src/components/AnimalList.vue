<template>
<div>
    <form @submit.prevent="addAnimal" class="form-class">
      <input placeholder="Specie" id="species" type="text" name="species" v-model="form.species"/>
      <input placeholder="Name" id="name" type="text" name="name" v-model="form.name" />
      <input placeholder="Birth" id="birth" type="hiden" name="birth" v-model="form.birth"/>
      <select v-model="form.selectedSector">
        <option v-bind:key="index" v-for="(sector, index) in sectors">{{sector}}</option>
      </select>      
      <button type="submit"> Add Animal </button>
    </form>
  <div>
    <table>
      <thead>
        <tr>
          <th>Species</th>
          <th>Name</th>
          <th>Birth</th>
          <th>Sector</th>
        </tr>
      </thead>
      <tbody>
        <tr v-bind:key="index" v-for="(value, index) in animals">
          <td>{{value.species}}</td>
          <td>{{value.name}}</td>
          <td v-if="!value.birth">Unknown</td>
          <td v-else-if="!value.birth.getFullYear">{{value.birth}}</td>
          <td v-else>{{value.birth.getFullYear()}}</td>
          <td>{{value.selectedSector}}</td>
          <td>
          <button @click="move(index)">Move to top </button>
          </td>
          <td>
          <button @click="remove(index)">Remove</button>
          </td>
        </tr>
      </tbody>
    </table>

    <table>
      <thead>
        <tr>
          <th>Sectors</th>
        </tr>
      </thead>
      <tbody>
        <tr v-bind:key="index" v-for="(sector, index) in sectors">
          <td>{{sector}}</td>
          <td>
            <button @click="viewAnimals(index)">View animal list</button>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</div>
</template>

<script>
export default {
  name: 'AnimalList',
  data() {
    return {
      animals: [
        {species: 'mammal', name: 'Dog', birth: new Date()},
        {species: 'bird', name: 'Parrot', birth: new Date()},
        {species: 'mammal', name: 'Cat', birth: new Date()},
        {species: 'fish', name: 'Tuna'},
        {species: 'bird', name: 'Pidgeon', birth: new Date()}
      ],

      form: {species: '', name: '', birth: '', selectedSector: ''},

      sectors: ['Snake', 'Bird', 'Mammal']
    }
    
  }, 

  methods: {
      remove(index) {
    this.$delete(this.animals, index)
    },

      move(index) {
        let animal = this.animals[index]
        this.remove(index)
        this.animals.unshift(animal)
      },

      addAnimal() {
        this.animals.push(this.form)
      },

      viewAnimals(index) {
        let listAnimals = this.animals.filter(animal =>
          animal.selectedSector == this.sectors[index]).map(animal => animal.species + " " + animal.name)

          alert(listAnimals)
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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

</style>
