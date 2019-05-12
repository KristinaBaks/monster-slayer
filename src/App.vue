<template>
  <div class="container">
    <h1 class="page-title">Beat the Monster!</h1>
    <section class="gamebars">
      <player-gamebar :changePlayerHealth="playerHealth"></player-gamebar>
      <monster-gamebar :changeMonsterHealth="monsterHealth"></monster-gamebar>
    </section>
    <controls-bar @attackedMonster="monsterHealth = $event"
                  @attackedPlayer="playerHealth = $event"
                  @specAttackedMonster="monsterHealth = $event"
                  @resetPlayerHealth="playerHealth = $event"
                  @resetMonsterHealth="monsterHealth = $event"
                  @attackMessage="turns = $event"></controls-bar>
    <log-section :turns="turns"></log-section>
  </div>
</template>

<script>
import playerGamebar from './components/playerGamebar'
import monsterGamebar from './components/monsterGamebar'
import controlsBar from './components/controlsBar'
import logSection from './components/logSection'

export default {
  components: {
    playerGamebar: playerGamebar,
    monsterGamebar: monsterGamebar,
    controlsBar: controlsBar,
    logSection: logSection
  },
  data () {
    return {
      playerHealth: 100,
      monsterHealth: 100,
      gameIsRunning: false,
      turns: []
      }
  }
}
</script>

<style lang="scss">
</style>
