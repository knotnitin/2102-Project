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
            <h3>{{ classItem.name }}</h3>
            <p>{{ classItem.description }}</p>
          </div>
          <button @click="addClass(classItem)">Add</button>
        </li>
      </ul>
    </section>

    <section>
      <h2>Classes I'm Taking</h2>
      <ul class="class-list">
        <li class="class-item" v-for="classItem in myClasses" :key="classItem.id">
          <div>
            <h3>{{ classItem.name }}</h3>
            <p>{{ classItem.description }}</p>
          </div>
          <button @click="removeClass(classItem)">Remove</button>
        </li>
      </ul>
    </section>
  </div>
</template>

  
  <script>
  export default {
    data() {
      return {
        allClasses: [
          { id: 1, name: 'Mathematics', description: 'Advanced calculus and algebra.' },
          { id: 2, name: 'History', description: 'World history from ancient times to the present.' },
          { id: 3, name: 'Computer Science', description: 'Introduction to programming and algorithms.' },
          // Add more class items as needed
        ],
        myClasses: [
          { id: 4, name: 'Physics', description: 'Mechanics, thermodynamics, and electromagnetism.' },
          { id: 5, name: 'English Literature', description: 'Classic and contemporary literature analysis.' },
          // Add more class items as needed
        ],
      };
    },
    methods: {
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
    }

  </style>
  