<template>
  <div>
    <div class="welcome-header">
      <div class="welcome-text">
        <h1 class="welcome-title">WELCOME</h1>
        <p class="welcome-subtitle">YOUR IPUMETO NALSEUR</p>
      </div>
      <div class="welcome-pattern">
        <div class="pattern-circle"></div>
        <div class="pattern-line pattern-line-1"></div>
        <div class="pattern-line pattern-line-2"></div>
        <div class="pattern-line pattern-line-3"></div>
        <div class="pattern-line pattern-line-4"></div>
        <div class="pattern-line pattern-line-5"></div>
        <div class="pattern-line pattern-line-6"></div>
      </div>
    </div>
    <div class="content-container">
      <div class="profile-section">
        <StudentProfile :student="student" @save="updateStudent" />
        <div class="image-grid">
          <img src="./photo/sahasap1.jpg" alt="รูปภาพ 1" class="grid-image" />
          <img src="./photo/Sahasap2.jpg" alt="รูปภาพ 2" class="grid-image" />
          <img src="./photo/sahasap3.jpg" alt="รูปภาพ 3" class="grid-image" />
        </div>
      </div>
      <div class="subject-section">
        <StdAdd
          :subjects="subjects"
          @add="addSubject"
          @update="updateSubject"
          @delete="deleteSubjectById"
          @remove="removeSubject"
        />
        <StdList
          :subjects="subjects"
          @save="saveSubject"
          @delete="deleteSubject"
        />
      </div>
    </div>
  </div>
</template>

<script>
import StudentProfile from "./components/StudentProfile.vue";
import StdAdd from "./components/StdAdd.vue";
import StdList from "./components/StdList.vue";

export default {
  components: {
    StudentProfile,
    StdAdd,
    StdList,
  },
  data() {
    return {
      student: {},
      subjects: [],
      editing: false,
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const studentResponse = await fetch("http://localhost:3000/students/1");
        this.student = await studentResponse.json();

        const subjectsResponse = await fetch("http://localhost:3000/subjects");
        this.subjects = await subjectsResponse.json();
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    async updateStudent(updatedStudent) {
      try {
        await fetch(`http://localhost:3000/students/${updatedStudent.id}`, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(updatedStudent),
        });
        this.fetchData();
      } catch (error) {
        console.error("Error updating student:", error);
      }
    },
    async saveSubject(editedSubject) {
      try {
        if (editedSubject.index !== undefined) {
          await fetch(`http://localhost:3000/subjects/${editedSubject.id}`, {
            method: "PUT",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify(editedSubject),
          });
        } else {
          await fetch("http://localhost:3000/subjects", {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify(editedSubject),
          });
        }
        this.fetchData();
      } catch (error) {
        console.error("Error saving subject:", error);
      }
    },
    async deleteSubject(index) {
      try {
        await fetch(`http://localhost:3000/subjects/${this.subjects[index].id}`, {
          method: "DELETE",
        });
        this.fetchData();
      } catch (error) {
        console.error("Error deleting subject:", error);
      }
    },
    async addSubject(subject) {
      try {
        await fetch("http://localhost:3000/subjects", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(subject),
        });
        this.fetchData();
      } catch (error) {
        console.error("Error adding subject:", error);
      }
    },
    async updateSubject(subject) {
      try {
        await fetch(`http://localhost:3000/subjects/${subject.id}`, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(subject),
        });
        this.fetchData();
      } catch (error) {
        console.error("Error updating subject:", error);
      }
    },
    async deleteSubjectById(id) {
      try {
        await fetch(`http://localhost:3000/subjects/${id}`, {
          method: "DELETE",
        });
        this.fetchData();
      } catch (error) {
        console.error("Error deleting subject by ID:", error);
      }
    },
    async removeSubject(index) {
      try {
        await fetch(`http://localhost:3000/subjects/${this.subjects[index].id}`, {
          method: "DELETE",
        });
        this.fetchData();
      } catch (error) {
        console.error("Error removing subject:", error);
      }
    },
    toggleEdit() {
      this.editing = !this.editing;
    },
  },
};
</script>

<style scoped>
.welcome-header {
  background: linear-gradient(to bottom, #f0f0f0, #e0e0e0);
  padding: 80px 0;
  text-align: center;
  position: relative;
  overflow: hidden;
  width: 100%;
  padding: 320px;
}

.welcome-text {
  position: relative;
  z-index: 1;
}

.welcome-title {
  font-size: 3em;
  font-weight: bold;
  color: #008080;
  margin-bottom: 10px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.welcome-subtitle {
  font-size: 1.2em;
  color: #008080;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

.welcome-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.pattern-circle {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #008080;
  opacity: 0.3;
}

.pattern-line {
  position: absolute;
  background-color: #008080;
  opacity: 0.2;
}

.pattern-line-1 {
  top: 10%;
  left: 5%;
  width: 50px;
  height: 1px;
}

.pattern-line-2 {
  top: 20%;
  right: 10%;
  width: 80px;
  height: 1px;
}

.pattern-line-3 {
  bottom: 15%;
  left: 15%;
  width: 120px;
  height: 1px;
}

.pattern-line-4 {
  bottom: 25%;
right: 20%;
  width: 60px;
  height: 1px;
}

.pattern-line-5 {
  top: 30%;
  left: 30%;
  width: 1px;
  height: 30px;
}

.pattern-line-6 {
  bottom: 30%;
  right: 30%;
  width: 1px;
  height: 40px;
}

.content-container {
  margin-top: 20px;
}

.profile-details {
  text-align: left;
  margin-bottom: 20px;
}

.profile-name {
  font-size: 1.8em;
  font-weight: bold;
  color: #333;
  margin-bottom: 5px;
}

.profile-info {
  font-size: 1em;
  color: #555;
  line-height: 1.6;
}

.edit-button {
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 15px;
}

.image-grid {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.grid-image {
  width: 200px;
  height: 200px;
  margin-bottom: 100px;
  object-fit: cover;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.grid-image:hover {
  transform: scale(1.1); 
}

@media (max-width: 768px) {
  .welcome-text {
    text-align: center;
  }

  .welcome-header {
    padding: 60px 0;
  }

  .image-grid {
    flex-direction: column;
    align-items: center;
  }

  .grid-image {
    width: 120px;
    height: 120px;
    margin-bottom: 10px;
  }
}
.content-container {
  background: linear-gradient(to bottom, #f0f0f0, #e0e0e0); /* เปลี่ยนพื้นหลังของ content-container */
  padding: 20px;
  border-radius: 8px; 
}
</style>