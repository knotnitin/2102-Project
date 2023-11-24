<template>
  <div>
    <header>
      <h1>Manage Classes</h1>
      <button class="logout-button" @click="logout">Logout</button>
    </header>

    <section>
      <button class="logout-button" @click="addClass">Add New Class</button>
      <h2>Classes I'm Teaching </h2>
      <ul id="class-list">
        <li class="class-item" v-for="classItem in allClasses" :key="classItem.id">
          <div>
            <h3>{{ classItem.courseid }}</h3>
            <p>{{ classItem.days + "  " + classItem.startTime + " - " + classItem.endTime }}</p>
            <p>{{ classItem.currentSize + " out of " + classItem.classSize + " seats filled" }}</p>
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
          console.log(classData)
          this.allClasses = classData

          // The code below is obsolete since I figured out how to show each class. I still wanna keep it here tho
          // const classList = document.getElementById("class-list") // list of all classes
          // for (var i=0; i< classData.length; i++){
          //   // console.log(classData[i])
          //   const liElement = document.createElement("li") // every list item that we add to ul
          //   const divElement = document.createElement("div") // this will hold all the details of each class
          //   const classTitle = document.createElement("h3") // class name
          //   classTitle.textContent = classData[i].courseid
          //   divElement.appendChild(classTitle)
          //   const classTime = document.createElement("p") // holds the class days and timing
          //   classTime.textContent = `${classData[i].days} ${classData[i].startTime} - ${classData[i].endTime}`
          //   divElement.appendChild(classTime)
          //   divElement.classList.add("class-item")
          //   // now add the div to the li
          //   liElement.appendChild(divElement)
          //   liElement.classList.add("class-item")
          //   classList.appendChild(liElement)
          // }
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
  
      .class-list {
        list-style: none;
        padding: 0;
      }

      /* Why this doesn't work is beyond me. It also broke the class-item thing below. */
  
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
    