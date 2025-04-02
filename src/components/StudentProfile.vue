<template>
  <div class="profile-container">
    <img src="../photo/sahsap.jpg" class="profile-image" alt="Profile Image" />
    <div class="profile-details">
      <h2 class="profile-name">{{ student.name }}</h2>
      <p class="profile-info">
        รหัส: {{ student.studentId }}<br />
        สาขา: {{ student.major }}<br />
        โรงเรียนเดิม: {{ student.school }}
      </p>
      <button class="edit-button" @click="toggleEdit">แก้ไขข้อมูล</button>
    </div>
    <StudentEdit
      v-if="editing"
      :student="student"
      @save="updateProfile"
      @cancel="cancelEdit"
    />
  </div>
</template>

<script>
import StudentEdit from "./StudentEdit.vue";

export default {
  components: {
    StudentEdit,
  },
  props: {
    student: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      editing: false,
    };
  },
  methods: {
    toggleEdit() {
      this.editing = !this.editing;
    },
    updateProfile(editedStudent) {
      this.$emit("save", editedStudent);
      this.editing = false;
    },
    cancelEdit() {
      this.editing = false;
    },
  },
};
</script>

<style scoped>
.profile-container {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 150px;
  gap: 20px;
}

.profile-image {
  width: 300px;
  height: 300px;
  object-fit: cover;
  border-radius: 50%;
}

.profile-details {
  text-align: left;
}

.profile-name {
  font-family: 'Arial', 'Helvetica', sans-serif;
  font-size: 2.5em;
  font-weight: bold;
  color: #333;
  margin-bottom: 10px;
}

.profile-info {
  font-family: 'Arial', 'Helvetica', sans-serif;
  font-size: 1.2em; 
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

@media (max-width: 768px) {
  .profile-container {
    flex-direction: column;
    padding: 20px;
  }

  .profile-image {
    width: 150px;
    height: 150px;
    margin: 0 0 20px 0;
  }

  .profile-name {
    font-size: 1.5em;
  }

  .profile-info {
    font-size: 1.1em;
  }

  .edit-button {
    padding: 8px 16px;
  }

  .profile-details {
    text-align: center;
  }
}
</style>