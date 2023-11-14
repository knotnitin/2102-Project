<template>
  <div>
    <div class="header">
      <h1 style="color:rgb(254, 255, 255);">UCONN Administrator Homepage</h1>
    </div>
    <div class="dashboard">
      <router-link to="/managescreen">
      <div class="box" @click="redirectToManageClasses">
        <div class="box-content">
          <h2>Manage Classes</h2>
          <img src="images/home1.jpeg" alt="Example 1" />
        </div>
      </div>
    </router-link>
      <div class="box" @click="redirectToScheduleGrades">
        <div class="box-content">
          <h2>Professor Schedule</h2>
          <img src="images/home2.jpeg" alt="Example 2" />
        </div>
      </div>
    </div>
    <router-link to="/">
    <button class="logout-button" @click="logout">Logout</button>
  </router-link>
  </div>
</template>

<script>
export default {
  methods: {
    redirectToManageClasses() {
      // Implement your logic to redirect to the Manage Classes page
    },
    redirectToScheduleGrades() {
      // Implement your logic to redirect to the Schedule and Grades page
    },
    logout() {
      // Implement your logout logic
    },
  },
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-image: url(./images/campus.jpeg);
  background-repeat: no-repeat;
  background-size:cover;
}
.header {
  background: #002D62; /* Navy blue */
  color: #ffffff;
  text-align: center;
  font-size: 30px;
  padding: 10px;
  font-weight: bold;
  text-decoration: none;
}
.dashboard {
  text-align: center;
  margin: 20px;
  text-decoration: none;
}
.box {
  width: 300px;
  height: 200px;
  background: #fff;
  color: #002D62;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin: 10px auto;
  cursor: pointer;
  display: block;
  text-decoration: none;
}
.box:hover {
  background: #d8f7ff; /* Lighter shade of blue */
}
.box-content {
  padding: 20px;
  font-weight: bold;
  text-decoration: none;
}
.box h2 {
  margin: 0;
  text-decoration: none;
}
.box img {
  max-width: 175px; /* Adjust the image size as needed */
  height: auto;
  margin-left: auto;
  margin-right: auto;
}
.logout-button {
  width: 120px;
  padding: 10px;
  background: #007BFF;
  border: none;
  color: #fff;
  border-radius: 5px;
  cursor: pointer;
  display: block;
  margin: 20px auto;
}
.logout-button:hover {
  background: #0056b3;
}
</style>