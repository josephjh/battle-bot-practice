<template>
  <div id='app'>
    <button @click='toggle(true)'>Create</button>      
    <h1>Battle Bots</h1>
    <button @click='toggle(false)'>Collection</button>
    
    <section v-if='showForm'>
      <input placeholder='Bot Name*' type="text" v-model="botName">
      <br>
      <input placeholder='Attack Value*' type="text" v-model="attack">
      <button @click='incrementAttack'>+</button>
      <button @click='decrementAttack'>-</button>
      <br>
      <input placeholder='Health Value*' type="text" v-model="health">
      <button @click='incrementHealth'>+</button>
      <button @click='decrementHealth'>-</button>
      <br>
      <button @click='addBot'>Add Bot</button>
      <button @click='clearForm'>Clear</button>
      <br>
    </section>
    
    <section v-else>
      
      <p>Bot #1: {{selectedBots[0]}}</p>
      <p>Bot #2: {{selectedBots[1]}}</p>
      <button @click='battle'>Battle</button>
      <button @click='clearSelected'>Clear</button>

      <hr>

      <bots v-for="(botObj, i) in allBots" 
      :key='i'
      :index='i'
      :bot-obj='botObj'
      :delete-bot='deleteBot'
      :select-bot='selectBot'
      />

    </section>
  </div>
</template>

<script>
import Bots from './components/Bots'

export default {
  name: 'app',
  data: function(){
    return {
      showForm: true,
      botName: '',
      attack:'',
      health:'',
      allBots:[],
      selectedBots:[]
    }
  },
  methods: {
    toggle: function(bool){
      this.showForm = bool
    },
    incrementAttack: function(){
      this.attack++
    },
    decrementAttack: function(){
      this.attack--
    },
    incrementHealth(){
      this.health++
    },
    decrementHealth(){
      this.health--
    },
    addBot: function(){
      const newBot = {botName: this.botName, attack: this.attack, health: this.health}
      this.allBots.push(newBot);
      this.botName='';
      this.attack='';
      this.health='';
      this.toggle()
    },
    clearForm: function(){
      this.botName='',
      this.attack='',
      this.health=''
    },
    deleteBot: function(i){
      this.allBots = this.allBots.filter((bot, index) => {
        return index !== i
      })
    },
    selectBot: function(obj){
     this.selectedBots.push(obj)
    },
    battle: function(){
      const victor = this.selectedBots[Math.floor(Math.random()*(1-0+1)+0)]
      return alert(`${victor} Wins!`)
    },
    clearSelected: function(){
      this.selectedBots= []
    }
  },
  components: {
    Bots: Bots
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
