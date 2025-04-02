<template>
  <div class="card edit-card">
    <div class="card-body">
      <h5 class="card-title">แก้ไขข้อมูลวิชา</h5>
      <form @submit.prevent="save">
        <div class="mb-3">
          <label for="editId" class="form-label">รหัสวิชา</label>
          <input type="text" class="form-control form-control-sm" id="editId" v-model="editedSubject.id">
        </div>
        <div class="mb-3">
          <label for="editName" class="form-label">ชื่อวิชา</label>
          <input type="text" class="form-control form-control-sm" id="editName" v-model="editedSubject.name">
        </div>
        <div class="mb-3">
          <label for="editGrade" class="form-label">เกรด</label>
          <select class="form-select form-select-sm" id="editGrade" v-model="editedSubject.grade">
            <option value="A">A</option>
            <option value="B+">B+</option>
            <option value="B">B</option>
            <option value="C+">C+</option>
            <option value="C">C</option>
            <option value="D+">D+</option>
            <option value="D">D</option>
            <option value="F">F</option>
          </select>
        </div>
        <div class="mb-3">
          <label for="editCredit" class="form-label">หน่วยกิต</label>
          <select class="form-select form-select-sm" id="editCredit" v-model="editedSubject.credit">
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
          </select>
        </div>
        <div class="d-flex justify-content-end">
          <button type="submit" class="btn btn-primary btn-sm me-2">บันทึก</button>
          <button type="button" class="btn btn-secondary btn-sm" @click="cancel">ยกเลิก</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    subject: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      editedSubject: { ...this.subject },
    };
  },
  methods: {
    save() {
      this.$emit("save", this.editedSubject);
    },
    cancel() {
      this.$emit("cancel");
    },
  },
};
</script>

<style scoped>
.edit-card {
  width: 500px;
  margin: 20px auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

.edit-card .card-body {
  padding: 20px;
}

.edit-card .card-title {
  margin-bottom: 20px;
  color: #333;
}

.edit-card .form-label {
  font-weight: bold;
}

.edit-card .form-control,
.edit-card .form-select {
  border-radius: 4px;
  border: 1px solid #ddd;
}

.edit-card .btn-primary {
  background-color: #42b983;
  border-color: #42b983;
}

.edit-card .btn-primary:hover {
  background-color: #42b983;
  border-color: #42b983;
}

.edit-card .btn-secondary {
  background-color: #6c757d;
  border-color: #6c757d;
}

.edit-card .btn-secondary:hover {
  background-color: #545b62;
  border-color: #545b62;
}
</style>