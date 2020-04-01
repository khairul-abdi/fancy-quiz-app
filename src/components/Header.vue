<template>
  <div>
    <b-nav tabs>
      <b-nav-item active disabled>
        <b>Fancy Quiz App</b>
      </b-nav-item>
      <b-nav-item class="info-answer" disabled>Question : {{ countQuestion }}/{{ totalQuestion }}</b-nav-item>
      <b-nav-item class="info-answer" disabled>Correct: {{ countCorrect }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: ["countCorrect", "totalQuestion", "countQuestion", "countAnswer"]
};
</script>

<style scoped>
.info-answer {
  position: relative;
  font-size: 14px;
  padding-bottom: 0 !important;
}
</style>
