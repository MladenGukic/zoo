<template>
<div>
  <div>
    <table>
      <thead>
        <tr>
          <th>Species</th>
          <th>Name</th>
          <th>Birth</th>
        </tr>
      </thead>
      <tbody>
        <tr v-bind:key="index" v-for="(value, index) in animals">
          <button @click="move(index)">Move to top </button>
          <td>{{value.species}}</td>
          <td>{{value.name}}</td>
          <td v-if="!value.birth">Nepoznato</td>
          <td v-else>{{value.birth.getFullYear()}}</td>
          <button @click="remove(index)">Remove</button>
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
        {species: 'mamml', name: 'King', birth: new Date()},
        {species: 'bird', name: 'Ko-ko', birth: new Date()},
        {species: 'mamml', name: 'Cleopatra', birth: new Date()},
        {species: 'fish', name: 'Joe'},
        {species: 'bird', name: 'Cleopatra', birth: new Date()}
      ]
    };
  }, 

  methods: {
      remove(index) {
    this.$delete(this.animals, index)
    },

      move(index) {
        let animal = this.animals[index]
        this.remove(index)
        this.animals.unshift(animal)
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
