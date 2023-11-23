<template>
  <div>
    <header>
      <h1>Manage Classes</h1>
      <button class="logout-button" @click="logout">Logout</button>
    </header>

    <section>
      <button @click="addClass">Add New Class</button>
      <h2>Classes I'm Teaching </h2>
      <ul id="class-list">
        
      </ul>
      <button @click="manageClass(classItem)">Manage</button>
    </section>
  </div>
</template>
  
    
    <script>

    import router from "@/router/index.js";
    
    export default {
      data() {
        return {
          // allClasses: [
          //   { id: 1, name: 'CSE 1729', description: 'Introduction to computer programming in a structured programming language including fundamental elements of program design and analysis.'},
          //   { id: 2, name: 'CSE 3100', description: 'Introduction to system-level programming with an emphasis on C programming, process management and small scale concurrency with multi-threaded programming.' },
          //   // Add more class items as needed
          // ],
          allClasses: []
        };
      },
      created() {
        // Call the getClassData method when the component is created
        this.getClassData();
      },
      methods: {
        async getClassData() {
          // get class data from database
          const response = await fetch(`https://d3euzpxjia.execute-api.us-east-1.amazonaws.com/prod/courses`, {
            method: "GET",
          })
          const responseData = await response.json();
          const classData = responseData.body
          console.log(classData) // responseData.body
          const classList = document.getElementById("class-list") // list of all classes

          for (var i=0; i< classData.length; i++){
            // console.log(classData[i])
            const liElement = document.createElement("li") // every list item that we add to ul
            const divElement = document.createElement("div") // this will hold all the details of each class
            const classTitle = document.createElement("h3") // class name
            classTitle.textContent = classData[i].courseName
            divElement.appendChild(classTitle)
            const classTime = document.createElement("p") // holds the class days and timing
            classTime.textContent = `${classData[i].days} ${classData[i].startTime} - ${classData[i].endTime}`
            divElement.appendChild(classTime)
            divElement.classList.add("class-item")
            // now add the div to the li
            liElement.appendChild(divElement)
            liElement.classList.add("class-item")
            classList.appendChild(liElement)
          }

          //return responseData.body
        },
        manageClass(classItem) {
          router.push({ name: 'professormanage', params: { id: classItem.id } });
        },

        logout() {
          this.$router.push('/')
        },

        addClass() {
          this.$router.push('/addclass')
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
        padding: 20px;
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

      .logout-button {
        width: 120px;
        padding: 5px;
        background: #007BFF;
        border: none;
        color: #fff;
        border-radius: 5px;
        cursor: pointer;
        display: block;
      }
      .logout-button:hover {
        background: #0056b3;
      }
  
      /* .class-list {
        list-style: none;
        padding: 0;
      } */
  
      .class-item {
        /* background-color: #e3efff;
        color: #002D62;
        border: 1px solid #ddd;
        margin: 10px 0;
        padding: 15px;
        display: flex;
        justify-content: space-between;
        align-items: center; */
        color: rebeccapurple;
      }


  
    </style>
    