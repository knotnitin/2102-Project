<template>
  <div>
    <header>
      <router-link to="/homescreen">
        <i class="fas fa-arrow-left"></i>
      </router-link>
      <h1>Manage Classes</h1>
    </header>

    <section>
      <h2>All Classes</h2>
      <ul class="class-list">
        <li class="class-item" v-for="classItem in canAdd_classes" :key="classItem.id">
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
              <h3>{{ classItem.courseid }}</h3>
              <p>{{ classItem.professor }}</p>
              <p>{{ classItem.days + "  " + classItem.startTime + " - " + classItem.endTime }}</p>
              <p>{{ classItem.currentSize + " out of " + classItem.classSize + " seats filled" }}</p>
            </div>
          </a>
            <button @click="removeClass(classItem)">Remove</button>
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
  </div>

</template>

  
  <script>
  export default {
    data() {
      return {
        allClasses: [], // Every single class
        canAdd_classes: [], // These classes can be added by the user
        // myClasses: [
        //   { id: 4, name: 'Physics', description: 'Mechanics, thermodynamics, and electromagnetism.' },
        //   { id: 5, name: 'English Literature', description: 'Classic and contemporary literature analysis.' },
        //   // Will update this later
        // ],
        myClasses: [], // The classes the user is taking
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
        this.allClasses = classData // Every single class

        // Get the list of classes the student is taking
        const response2 = await fetch(`https://d3euzpxjia.execute-api.us-east-1.amazonaws.com/prod/login?username=jhu20000`, { // Hardcoded, will fix later
            method: "GET",
        })
        const responseData2 = await response2.json();
        // console.log(responseData2)
        const userClasses = responseData2.body.Item.coursesTaken
        // console.log(userClasses)
        // Call updateClasses
        this.updateClasses(userClasses)
      },

      async addClass(classItem) {
        // Logic to add a class to 'myClasses' array
        const index = this.allClasses.indexOf(classItem)
        const currentClass = this.allClasses[index].courseid // The class we want to move from one array to another
        console.log("adding this class to coursesTaken ", currentClass)
        const payload = {
          username: "jhu20000", // Hardcoding this right now, but this is not an efficient way of doing things and needs to be changed
          course: currentClass,
          action: "ADD"
        }
        const response = await fetch('https://d3euzpxjia.execute-api.us-east-1.amazonaws.com/prod/courses', {
          method: "PUT",
          body: JSON.stringify(payload),
          headers: {
            'Content-Type': 'application/json',
          },
        })
        const responseData = await response.json();
        console.log(responseData)
        // Update class lists IF statusCode was 200
        if(responseData.statusCode == 200){
          this.updateClasses(responseData.body)
        }
      },

      async removeClass(classItem) {
        // Logic to remove a class from 'myClasses' array
        const index = this.allClasses.indexOf(classItem)
        const currentClass = this.allClasses[index].courseid // The class we want to move from one array to another
        console.log("removing this class from coursesTaken ", currentClass)
        const payload = {
          username: "jhu20000", // Hardcoding this right now, but this is not an efficient way of doing things and needs to be changed
          course: currentClass,
          action: "DELETE"
        }
        const response = await fetch('https://d3euzpxjia.execute-api.us-east-1.amazonaws.com/prod/courses', {
          method: "PUT",
          body: JSON.stringify(payload),
          headers: {
            'Content-Type': 'application/json',
          },
        })
        const responseData = await response.json();
        console.log(responseData)
        // Update class lists IF statusCode was 200
        if(responseData.statusCode == 200){
          this.updateClasses(responseData.body)
        }
      },

      updateClasses(userClassList){
        // Updating canAdd_classes and myClasses everytime a new class is added/dropped, and also when the webpage is loaded for the first time
        // console.log(this.allClasses)
        // console.log(userClassList)
        this.canAdd_classes = [] // reset
        this.myClasses = [] // reset

        // Now we filter allClasses into 2 sections: Classes the user is taking, and classes they aren't taking
        for (var i=0; i<this.allClasses.length; i++){
          // console.log(this.allClasses[i].courseid)
          if(userClassList.includes(this.allClasses[i].courseid)){ // this.allClasses[i].courseid in userClassList
            // Put this class in myClasses
            this.myClasses.push(this.allClasses[i])
          }
          else{
            this.canAdd_classes.push(this.allClasses[i])
          }
        }
        // Debugging: Printing out the entirety of canAdd and myClasses
        // console.log(this.canAdd_classes)
        // console.log(this.myClasses)
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
      background: #002D62;
      padding: 10px;
      text-align: center;
    }
    header i{
      color:white;
      margin-left: 10px;
    }

    header h1{
      font-size: 35px;
      color: white;
      margin-left: auto;
      margin-right: auto;
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

  </style>
  
