<template>
  <div class="square">
    <div class="sun">
      <div class="dot">🤮</div>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.sun {
  width: 300px;
  height: 300px;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  animation-name: orbit;
  animation-duration: 2s;
  border-radius: 50%;
  border: solid 2px hsla(160, 100%, 37%, 0.5);
}

.dot {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 5rem;
  top: 0;
  left: 0;
  width: 115px;
  height: 115px;
  background: hsla(160, 100%, 37%, 0.8);
}

@keyframes orbit {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
