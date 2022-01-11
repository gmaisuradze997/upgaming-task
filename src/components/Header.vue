<template>
  <div class="header-container">
    <img class="logo" src="../assets/logo.png" alt="logo" />
    <ul class="navigation">
      <li><a href="#home">Sports</a></li>
      <li><a href="#news">In-Play</a></li>
      <li><a href="#contact">Casino</a></li>
      <li><a href="#about">Live Casino</a></li>
      <li><a href="#about">Virtual Sports</a></li>
    </ul>
    <div class="login-container">
      <button class="btn sign-up-btn">Join</button>
      <button class="btn log-in-btn">Log In</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "Header",
};
</script>
<style scoped lang="scss">
.header-container {
  height: 75px;
  width: 100%;
  background-color: #1c1c1c;
  .logo {
    margin-top: 20px;
    margin-left: 50px;
    margin-right: 50px;
    float: left;
  }
  .navigation {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    margin-left: 50px;
    width: 650px;
    li {
      float: left;
      height: 75px;
      padding-top: 20px;
      width: 125px;
      a {
        display: block;
        padding: 8px;
        text-decoration: none;
        font-family: Poppins;
        font-size: 15px;
        color: white;
      }
    }
  }
  .login-container {
    height: 75px;
    position: absolute;
    top: 20px;
    right: 20px;
    .btn {
      width: 72px;
      height: 32px;
      background-color: #fff209;
      outline: none;
      cursor: pointer;
      border-radius: 4px;
      border: none;
      margin-right: 25px;
      font-family: Poppins;
    }
    .sign-up-btn {
      background-color: #fff209;
    }
    .log-in-btn {
      background-color: #1c1c1c;
      color: white;
    }
  }
}
</style>
