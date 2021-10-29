<template>
  <header class="flex">
    <div class="flex">
      <a href="#"><img src="../assets/logo.svg" alt="Logo Sneakers" /></a>
      <nav>
        <ul class="flex">
          <li><a href="#">Collections</a></li>
          <li><a href="#">Men</a></li>
          <li><a href="#">Women</a></li>
          <li><a href="#">About</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </nav>
    </div>
    <div class="info flex">
      <a href="#"><img src="../assets/icon-cart.svg" alt="Cart" /></a>
      <a href="#" class="avatar"
        ><img src="../assets/image-avatar.png" alt="User"
      /></a>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style lang="scss" scoped>
.flex {
  display: flex;
  align-items: center;
}

header {
  justify-content: space-between;
  padding: 30px 0;
  border-bottom: 1px solid hsl(220, 14%, 90%);
}

nav ul {
  margin-left: 40px;

  a {
    color: hsl(219, 9%, 45%);
    margin-left: 15px;
    padding: 10px;
    transition: color 0.3s;

    &:hover {
      color: hsl(220, 13%, 13%);
    }
  }
}

.avatar {
  max-width: 45px;
  margin-left: 40px;
}
</style>
