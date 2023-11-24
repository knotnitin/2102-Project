<template>
  <div>
    <header>
      <h1>Manage Classes</h1>
    </header>

    <section>
      <h2>All Classes</h2>
      <ul class="class-list">
        <li class="class-item" v-for="classItem in allClasses" :key="classItem.id">
          <div>
            <h3>{{ classItem.courseid }}</h3>
            <p>{{ classItem.professor }}</p>
            <p>{{ classItem.days + "  " + classItem.startTime + " - " + classItem.endTime }}</p>
            <p>{{ classItem.currentSize + " out of " + classItem.classSize + " seats filled" }}</p>
          </div>
          <button @click="addClass(classItem)">Add</button>
        </li>
      </ul>
    </section>

    <section>
      <h2>Your Current Classes</h2>
      <ul class="class-list">
        <li class="class-item" v-for="classItem in myClasses" :key="classItem.id">
          <a @click="removeClass(classItem)" style="cursor: pointer;">
            <div>
              <h3>{{ classItem.name }}</h3>
              <p>{{ classItem.description }}</p>
            </div>
          </a>
            <button>Remove</button>
        </li>
      </ul>
    </section>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <h2>{{ selectedClass.name }}</h2>
        <p>{{ selectedClass.description }}</p>
        <button @click="closeClassModal">Close</button>
      </div>
    </div>

    <section class="back-button-section">
      <router-link to="/homescreen">
      <button class="back-button" @click="goBack">Back</button>
    </router-link>
    </section>
  </div>

</template>

  
  <script>
  export default {
    data() {
      return {
        allClasses: [],
        myClasses: [
          { id: 4, name: 'Physics', description: 'Mechanics, thermodynamics, and electromagnetism.' },
          { id: 5, name: 'English Literature', description: 'Classic and contemporary literature analysis.' },
          // Will update this later
        ],
      };  
  },
  created() {
        // Call the getClassData method when the component is created
        this.getData();
      },
    methods: {
      async getData(){
        const response = await fetch(`https://d3euzpxjia.execute-api.us-east-1.amazonaws.com/prod/courses`, {
            method: "GET",
          })
        const responseData = await response.json();
        const classData = responseData.body
        console.log(classData) // responseData.body
        this.allClasses = classData
      },
      addClass(classItem) {
        // Logic to add a class to 'myClasses' array
        // You can implement this logic here
      },
      removeClass(classItem) {
        // Logic to remove a class from 'myClasses' array
        // You can implement this logic here
      },
  },
};
  </script>
  
  <style scoped>
     body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #002D62;
      color: white;
      padding: 10px;
      text-align: center;
    }

    header h1{
      font-size: 35px;
      color: white;
    }
    section h2{
      font-size: 20px;
      color: black;
      font-weight: bold;
    }
    section {
      margin: 20px;
      color: #002D62
    }

    .class-list {
      list-style: none;
      padding: 0;
    }

    .class-item {
      background-color: #e3efff;
      color: #002D62;
      border: 1px solid #ddd;
      margin: 10px 0;
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 17px;
    }
    button {
    width: 175px;
    background: #007BFF;
    border: none;
    color: #fff;
    padding: 10px;
    border-radius: 100px;
    cursor: pointer;
    text-align: center;
    display: block;
  }
  
  button:hover {
    background: #0056b3;
  }

.back-button {
  width: 120px;
  background: #007BFF;
  border: none;
  color: #fff;
  padding: 10px;
  border-radius: 100px;
  cursor: pointer;
  text-align: center;
  display: block;
  margin: 20px auto;
  margin-top: 50px;
}

a:hover {
  background: #d8f7ff; /* Lighter shade of blue */
}

  </style>
  