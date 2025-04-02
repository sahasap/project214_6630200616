<template>
  <div class="edit-student-form">
    <h2>แก้ไขข้อมูลนิสิต</h2>
    <div class="form-group">
      <label for="name">ชื่อ-นามสกุล:</label>
      <input type="text" id="name" v-model="editedStudent.name" />
    </div>
    <div class="form-group">
      <label for="studentId">รหัสนิสิต:</label>
      <input type="text" id="studentId" v-model="editedStudent.studentId" />
    </div>
    <div class="form-group">
      <label for="major">สาขาวิชา:</label>
      <input type="text" id="major" v-model="editedStudent.major" />
    </div>
    <div class="form-group">
      <label for="school">โรงเรียน:</label>
      <input type="text" id="school" v-model="editedStudent.school" />
    </div>
    <div class="form-actions">
      <button class="save-button" @click="save">บันทึก</button>
      <button class="cancel-button" @click="cancel">ยกเลิก</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    student: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      editedStudent: { ...this.student },
    };
  },
  methods: {
    save() {
      this.$emit("save", this.editedStudent);
    },
    cancel() {
      this.$emit("cancel");
    },
  },
};
</script>

<style scoped>
.edit-student-form {
  border: 2px solid #42b983;
  padding: 30px;
  border-radius: 10px;
  width: 500px;
  margin: 30px auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

h2 {
  color: #35495e;
  text-align: center;
  margin-bottom: 25px;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  color: #35495e;
  font-weight: 600;
  font-family: 'Arial', 'Helvetica', sans-serif; 
  font-size: 1em; 
}

input[type="text"] {
  width: calc(100% - 18px);
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 1em;
  transition: border-color 0.3s ease;
  font-family: 'Arial', 'Helvetica', sans-serif; 
  color: #555; 
}

input[type="text"]:focus {
  border-color: #42b983;
  outline: none;
}

.form-actions {
  text-align: right;
  margin-top: 25px;
}

button {
  padding: 12px 20px;
  margin-left: 15px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1em;
  transition: background-color 0.3s ease;
}

.save-button {
  background-color: #42b983;
  color: white;
}

.save-button:hover {
  background-color: #389772;
}

.cancel-button {
  background-color: #6c757d;
  color: white;
}

.cancel-button:hover {
  background-color: #5a6268;
}

@media (max-width: 768px) {
  .edit-student-form {
    width: 90%;
    padding: 15px;
  }

  h2 {
    font-size: 1.2em;
  }

  label {
    font-size: 0.9em;
  }

  input[type="text"] {
    padding: 6px;
  }

  button {
    padding: 6px 12px;
    font-size: 0.9em;
  }
}
</style>