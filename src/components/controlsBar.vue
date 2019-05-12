<template>
    <section class="controls-bar">
        <section class="controls" v-if="!gameIsRunning">
            <div class="">
                <button class="start-game" @click="startGame">START NEW GAME</button>
            </div>
        </section>
        <section class="controls" v-else>
            <div class="">
                <button class="attack" @click="attack">ATTACK</button>
                <button class="special-attack" @click="specialAttack">SPECIAL ATTACK</button>
                <button class="heal" @click="heal">HEAL</button>
                <button class="give-up" @click="giveUp">GIVE UP</button>
            </div>
        </section>
    </section>
</template>

<script>
import playerGamebar from './playerGamebar'
import monsterGamebar from './monsterGamebar'

export default {
    data () {
      return {
        playerHealth: 100,
        monsterHealth: 100,
        gameIsRunning: false,
        turns: []
        }
    },
    methods: {
        startGame (){
            this.gameIsRunning = true; // controls the display of buttons
            this.playerHealth = 100; // resets the bar
            this.monsterHealth = 100; // resets the bar
            this.turns = [];

            this.$emit('resetPlayerHealth', this.playerHealth);
            this.$emit('resetMonsterHealth', this.monsterHealth);
            this.$emit('attackMessage', this.turns);
        },
        attack () {
            var damage = this.calculateDamage(3, 10);
            this.monsterHealth -= damage;
            this.turns.unshift({
                isPlayer: true,
                text: 'Player hits Monster for ' + damage
            });
            if (this.checkWin()) {
                return;
            }
            this.$emit('attackedMonster', this.monsterHealth);

            this.monsterAttacks();
        },
        specialAttack () {
            var damage = this.calculateDamage(10, 20);
            this.monsterHealth -= damage;

            this.turns.unshift({
                isPlayer: true,
                text: 'Player superhits Monster for ' + damage
            });

            if (this.checkWin()) {
                return;
            }
            this.$emit('specAttackedMonster', this.monsterHealth);

            this.monsterAttacks();
        },
        heal () {
            if (this.playerHealth <= 90) {
                this.playerHealth += 10;
            } else {
                this.playerHealth = 100;
            }
            this.turns.unshift({
                isPlayer: true,
                text: 'Player heals  for 10'
            });
            this.monsterAttacks(); // monster still attacks
        },
        giveUp () {
            this.gameIsRunning = false; // control the display of buttons but no reload
        },
        monsterAttacks () {
            var damage = this.calculateDamage(5, 12);
            this.playerHealth -= damage;
            this.checkWin();
            this.turns.unshift({
                isPlayer: false,
                text: 'Monster hits Player for ' + damage
            });

            this.$emit('attackedPlayer', this.playerHealth);
        },
        calculateDamage (min, max) {
            return Math.max(Math.floor(Math.random() * max) + 1, min);
        },
        checkWin () {
            if (this.monsterHealth <= 0) {
                if (confirm('You won. New Game?')) {
                    this.startGame();
                } else {
                    this.gameIsRunning = false;
                }
                return true;
            } else if (this.playerHealth <= 0) {
                if (confirm('You lost. New Game?')) {
                    this.startGame();
                } else {
                    this.gameIsRunning = false;
                }
                return true;
            }
            return false;
        }
    }
}
</script>