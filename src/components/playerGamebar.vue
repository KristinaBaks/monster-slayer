<template>
  <div class="gamebar">
    <h1 class="gamebar__name">YOU</h1>
    <div class="gamebar__healthbar">
      <div class="gamebar__healthbar-top" :style="{width: changePlayerHealth + '%'}">
        <p class="gamebar__healthbar-top--text">{{ changePlayerHealth }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    changePlayerHealth: Number
  }
};
</script>
