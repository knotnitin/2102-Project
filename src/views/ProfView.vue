<template>
  <div>
    <header>
      <h1>Manage Classes</h1>
      <button class="logout-button" @click="logout">Logout</button>
    </header>

    <section>
      <h2>Classes I'm Teaching </h2>
      <ul class="class-list">
        <li class="class-item" v-for="classItem in allClasses" :key="classItem.id">
          <div>
            <h3>{{ classItem.name }}</h3>
            <p>{{ classItem.description }}</p>
          </div>
          <button @click="manageClass(classItem)">Manage</button>
        </li>
      </ul>
    </section>
  </div>
</template>
  
    
    <script>

    import router from "@/router/index.js";
    
    export default {
      data() {
        return {
          allClasses: [
            { id: 1, name: 'CSE 1729', description: 'Introduction to computer programming in a structured programming language including fundamental elements of program design and analysis.'},
            { id: 2, name: 'CSE 3100', description: 'Introduction to system-level programming with an emphasis on C programming, process management and small scale concurrency with multi-threaded programming.' },
            // Add more class items as needed
          ],
        };
      },
      methods: {
        manageClass(classItem) {
          router.push({ name: 'professormanage', params: { id: classItem.id } });
        },

        logout() {
          router.push({ name: 'login', params: { id: classItem.id } });
        }
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
    