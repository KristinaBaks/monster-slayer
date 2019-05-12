<template>
    <section class="log" v-if="turns.length > 1">
        <div class="">
            <ul>
                <li v-for="turn in turns"
                    :class="{'player-turn': turn.isPlayer, 'monster-turn': !turn.isPlayer}">
                    {{ turn.text }}
                </li>
            </ul>
        </div>
    </section>
</template>

<script>
export default {
    props: ['turns']
}
</script>
