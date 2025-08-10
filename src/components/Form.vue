<template>
  <h1>Student Infomation</h1>
  <form @submit.prevent="ShowData(index)">
    <label for="name" >Name:</label>
    <input type="text" v-model="studentData.name" /><br />
    <label for="gender">Gender:</label>

    <input name="gender" v-model="studentData.gender" type="radio" id="male" value="Male" />
    <label for="male">Male</label><br />

    <input name="gender" type="radio" id="female" value="Female" v-model="studentData.gender"/>
    <label for="female">Female</label><br />

    <label for="age">Age:</label><br />
    <input type="number" id="age" v-model="studentData.age"/><br /><br />

    
    <label for="subject">Subject:</label><br />
    <select id="subject" v-model="studentData.subject">
      <option value="" disabled>--Please choose an option--</option>
      <option value="Math">Math</option>
      <option value="Science">Science</option>
      <option value="English">English</option>
      <option value="History">History</option></select
    ><br /><br />

    <button type="submit">Submit</button>
  </form>

  <h1 v-if="isShow">Card</h1>
  <ul>
  <li v-if="isShow" v-for="(student, index) in Students" :key="index">
    Name: {{ student.name }}, Gender: {{ student.gender }}, Age: {{ student.age }}, Subject: {{ student.subject }}
    <button class="edit-btn" @click="editStudent(index)">Edit</button>
    <button class="delete-btn" @click="deleteStudent(index)">Delete</button>
  </li>
</ul>


</template>


<script>
export default {
  name: "Form",
  data () {
    return {
        studentData : {
            name : "",
            gender : "",
            age : null,
            subject : "",
            
        },
        isShow : false,
        Students : [],
        isEdit : false,
        tempEdit : null,
    }
  },
  methods: {
    ShowData () {
    if(this.studentData.name == "" || this.studentData.gender == "" || this.studentData.age == "" || this.studentData.subject == ""){
      alert("Please fill all data")
    }
    else if(this.Students[this.tempEdit]) {
      this.Students[this.tempEdit].name = this.studentData.name;
      this.Students[this.tempEdit].gender = this.studentData.gender;
      this.Students[this.tempEdit].age = this.studentData.age;
      this.Students[this.tempEdit].subject = this.studentData.subject;
      
      this.studentData.name = "";
      this.studentData.gender = "";
      this.studentData.age = null;
      this.studentData.subject = "";
      this.tempEdit = null;
    }
    else{
      this.isShow = true;
      this.Students.push({ ...this.studentData });
      this.studentData.name = "";
      this.studentData.gender = "";
      this.studentData.age = null;
      this.studentData.subject = "";
    }
        
    },
    deleteStudent(index) {
    this.Students.splice(index, 1);
    console.log(index);
  },
  editStudent(index){
    this.studentData.name = this.Students[index].name;
      this.studentData.gender = this.Students[index].gender;
      this.studentData.age = this.Students[index].age;
      this.studentData.subject = this.Students[index].subject;
      this.tempEdit = index;
  },
  }
};
</script>

<style scoped>
  h1 {
    color: #2c3e50;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin-bottom: 1rem;
  }

  form {
    max-width: 400px;
    background-color: #f7f9fc;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    font-family: Arial, sans-serif;
  }

  label {
    font-weight: 600;
    display: block;
    margin-bottom: 6px;
    color: #34495e;
  }

  input[type="text"],
  input[type="number"],
  select {
    width: 100%;
    padding: 8px 10px;
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    font-size: 14px;
  }

  input[type="radio"] {
    margin-right: 6px;
  }

  button {
    background-color: #3498db;
    color: white;
    padding: 10px 16px;
    border: none;
    border-radius: 5px;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #2980b9;
  }

  ul {
    max-width: 400px;
    margin-top: 20px;
    padding-left: 20px;
    font-family: Arial, sans-serif;
  }

  li {
    background-color: #ecf0f1;
    padding: 10px;
    margin-bottom: 8px;
    border-radius: 5px;
    color: #2c3e50;
  }
  .delete-btn {
  background-color: #e74c3c;
  border: none;
  color: white;
  padding: 5px 10px;
  margin-left: 12px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  transition: background-color 0.2s ease;
}

.delete-btn:hover {
  background-color: #c0392b;
}

.edit-btn {
  background-color: #3ce7e7;
  border: none;
  color: white;
  padding: 5px 10px;
  margin-left: 12px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  transition: background-color 0.2s ease;
}

.edit-btn:hover {
  background-color: #00cdcd;
}

</style>

