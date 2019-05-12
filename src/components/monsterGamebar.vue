<template>
    <div class="gamebar">
        <h1 class="gamebar__name">MONSTER</h1>
        <div class="gamebar__healthbar">
            <div class="gamebar__healthbar-top"
                :style="{width: changeMonsterHealth + '%'}">
                <p class="gamebar__healthbar-top--text">{{ changeMonsterHealth }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        changeMonsterHealth: Number
    }
}
</script>
