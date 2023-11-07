<template>
  <div> 
    <header>
      <h1 style="color:rgb(254, 255, 255);">Welcome to UCONN Student Admin</h1>
      <div class="header-buttons">
        <router-link to="/login">
          <button class="login-button">
            Login
          </button>
        </router-link>

        <div class="search-icon" @click="openSearch">
          <i class="fas fa-search"></i>
        </div>
      </div>
    </header>
    <body>
      <div id="slides">
      <div class="overlay"></div>

      <div class="slides-container">
        <img src="/images/campus.jpeg" alt="">
      </div>
      </div>
    </body>
  </div>
</template>

<script>
export default {
  methods: {
    openSearch() {
      // Implement your search functionality here
      // This function could show a search bar or open a search modal.
    }
  }
}
</script>

<style>
/* Add your CSS styles here */
header {
  background-color: #0074bf;
  background-image: linear-gradient(#000E2F, #0074bf);
  color: white;
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 25px;
  font-weight: bolder;

}

.login-button {
  background-color: #ef620b;
  color: white;
  border: none;
  padding: 10px 30px;
  cursor: pointer;
  border-radius: 30px;
}

a {
    text-decoration: none;
}

.login-button:hover {
  background-color: #f23c0a;
}

.header-buttons {
  display: flex;
  align-items: center;
}

.search-icon {
  cursor: pointer;
  padding: 10px 20px;
}
</style>
