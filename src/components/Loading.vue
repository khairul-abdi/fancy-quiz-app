<template>
  <div>
    <h3 class="blinking">Loading</h3>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
div {
  position: relative;
  z-index: 1;
  margin-top: -3px;
  padding-bottom: 15px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: #e9ecef;
}

.blinking {
  animation: blinkingText 0.7s infinite;
}

@keyframes blinkingText {
  0% {
    color: #000;
  }
  49% {
    color: #000;
  }
  60% {
    color: transparent;
  }
  99% {
    color: transparent;
  }
  100% {
    color: #000;
  }
}
</style>