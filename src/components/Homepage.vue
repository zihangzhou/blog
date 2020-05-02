<template>
  <div>
    <img
      class="img-wrap"
      alt="route66 sign"
      style="left: 50px;"
      src="../assets/route66.png"
    />
    <img alt="car" src="../assets/car.png" />
    <img
      class="img-wrap"
      alt="stop sign"
      style="right: 50px;"
      src="../assets/stop.png"
    />
    <h1>Welcome to the land of mystery!</h1>
  </div>
</template>

<script>
export default {};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h1 {
  text-align: center;
  color: blue;
}

img {
  border-radius: 10px;
}

.img-wrap {
  width: 250px;
  height: 250px;
  position: fixed;
  top: 100px;
}
</style>
