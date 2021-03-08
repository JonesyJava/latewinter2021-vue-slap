<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div v-for="character in state.characters" :key="character.name">
  <h1 :class="statusColor(character)">{{character.name}}</h1>
  <h3 class="text-success" :class="{'text-warning': character.health < 50, 'text-danger': character.health < 20}">{{character.health}}</h3>
  <button class="btn btn-danger m-1" @click="attackCharacter(character, attackName)" :disabled="character.health < 1" v-for="( attack, attackName) in character.attacks" :key="attackName">{{attackName}}</button>
  </div>
</template>

<script>
import { reactive } from 'vue'

export default {
  name: 'App',
  setup () {
    const state = reactive({
      characters: [{
        name: 'Bob',
        health: 100,
        attacks: {
          slap: 1,
          punch: 5
        }
      },
      {
        name: 'The other Bob',
        health: 100,
        attacks: {
          'Eye Gouge': 1,
          pocketSand: 0,
          shinKick: 15
        }
      }]
    })
    // for (let i = 0; i < 100; i++) {
    //   state.characters.push({
    //     name: 'The other Bob' + i,
    //     health: 100
    //   })
    // }
    return {
      state,
      statusColor (char) {
        let cssClass = 'text-success'
        if (char.health < 20) {
          cssClass = 'text-danger'
        } else if (char.health < 50) {
          cssClass = 'text-warning'
        }
        return cssClass
      },
      attackCharacter (character, key) {
        character.health = character.health - character.attacks[key] < 0 ? 0 : character.health -= character.attacks[key]
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
