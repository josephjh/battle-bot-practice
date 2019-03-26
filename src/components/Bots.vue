<template>
    <div>
      <p>{{botObj.botName}}</p>
      <p>{{botObj.attack}}</p>
      <p>{{botObj.health}}</p>
      <button @click='deleteBot(index)'>Retire</button> 
      <button @click='selectBot(botObj.botName)'>Select</button> 
    </div>
   
</template>

<script>
export default {
    props: ['botObj', 'index', 'deleteBot', 'selectBot'],
}
</script>
