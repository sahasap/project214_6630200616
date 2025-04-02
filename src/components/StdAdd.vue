<template>
  <div class="card add-subject-card">
    <div class="card-body">
      <button @click="toggleSubjectForm" class="btn btn-primary mt-4">เพิ่มรายวิชา</button>
      <div v-if="showSubjectForm" class="add-subject-form">
        <h3 class="mb-4 text-center">เพิ่มรายวิชา</h3>
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="row">
                  <div class="col-lg-6 col-md-6 col-sm-12 mt-2">
                    <label for="subjectIdAdd" class="form-label">รหัสวิชา</label>
                    <input type="text" id="subjectIdAdd" class="form-control form-control-sm" v-model.trim="subjectData.id" />
                  </div>
                  <div class="col-lg-6 col-md-6 col-sm-12 mt-2">
                    <label for="subjectNameAdd" class="form-label">ชื่อวิชา</label>
                    <input type="text" id="subjectNameAdd" class="form-control form-control-sm" v-model.trim="subjectData.name" />
                  </div>
                  <div class="col-lg-6 col-md-6 col-sm-12 mt-2">
                    <label for="subjectGradeAdd" class="form-label">เกรด</label>
                    <select id="subjectGradeAdd" class="form-select form-select-sm" v-model="subjectData.grade">
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
                  <div class="col-lg-6 col-md-6 col-sm-12 mt-2">
                    <label for="subjectCreditAdd" class="form-label">หน่วยกิต</label>
                    <select id="subjectCreditAdd" class="form-select form-select-sm" v-model="subjectData.credit">
                      <option value="1">1</option>
                      <option value="2">2</option>
                      <option value="3">3</option>
                      <option value="4">4</option>
                      <option value="5">5</option>
                      <option value="6">6</option>
                    </select>
                  </div>
                </div>
                <div class="mt-4 d-flex justify-content-center">
                  <button @click="addSubject" class="btn btn-success btn-sm mx-2">เพิ่ม</button>
                  <button @click="deleteSubject" class="btn btn-danger btn-sm mx-2">ลบ</button>
                </div>
              </div>
              <div class="col-lg-6">
                <table class="table table-sm mt-2 table-striped">
                  <thead>
                    <tr>
                      <th>รหัสวิชา</th>
                      <th>ชื่อวิชา</th>
                      <th>เกรด</th>
                      <th>หน่วยกิต</th>
                      <th>การกระทำ</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(subject, index) in subjects" :key="index">
                      <td>{{ subject.id }}</td>
                      <td>{{ subject.name }}</td>
                      <td>{{ subject.grade }}</td>
                      <td>{{ subject.credit }}</td>
                      <td>
                        <button @click="editSubject(index)" class="btn btn-sm btn-warning mx-1">แก้ไข</button>
                        <button @click="removeSubject(index)" class="btn btn-sm btn-danger mx-1">ลบ</button>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StdAdd.vue",
  props: {
    subjects: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      subjectData: {
        id: null,
        name: null,
        grade: null,
        credit: null,
      },
      showSubjectForm: false,
      editIndex: null,
    };
  },
  methods: {
    toggleSubjectForm() {
      this.showSubjectForm = !this.showSubjectForm;
    },
    addSubject() {
      if (this.subjectData.id) {
        this.$emit("add", { ...this.subjectData });
        this.clearSubjectData();
      }
    },
    updateSubject() {
      if (this.editIndex !== null) {
        this.$emit("update", { ...this.subjectData, index: this.editIndex });
        this.clearSubjectData();
        this.editIndex = null;
      }
    },
    deleteSubject() {
      if (this.subjectData.id) {
        this.$emit("delete", this.subjectData.id);
        this.clearSubjectData();
      }
    },
    editSubject(index) {
      this.subjectData = { ...this.subjects[index] };
      this.editIndex = index;
    },
    removeSubject(index) {
      this.$emit("remove", index);
    },
    clearSubjectData() {
      this.subjectData = {
        id: null,
        name: null,
        grade: null,
        credit: null,
      };
    },
  },
};
</script>

<style scoped>
.add-subject-card {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

.add-subject-form {
  margin-top: 20px;
  padding: 20px;
  border-radius: 8px;
}

.table th,
.table td {
  text-align: center;
}

.table-striped tbody tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
</style>