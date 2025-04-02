<template>
  <div>
    <table class="subject-table">
      <thead>
        <tr>
          <th>รหัสวิชา</th>
          <th>ชื่อวิชา</th>
          <th>เกรด</th>
          <th>หน่วยกิต</th>
          <th>แก้ไขข้อมูล</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(subject, index) in subjects" :key="index">
          <td>{{ subject.id }}</td>
          <td>{{ subject.name }}</td>
          <td>{{ subject.grade }}</td>
          <td>{{ subject.credit }}</td>
          <td>
            <button class="btn btn-primary btn-sm" @click="editSubject(index)">แก้ไข</button>
            <button class="btn btn-danger btn-sm" @click="deleteSubject(index)">ลบ</button>
          </td>
        </tr>
      </tbody>
    </table>
    <StdEdit v-if="editingSubject" :subject="editingSubject" @save="saveSubject" @cancel="cancelEdit" />
  </div>
</template>

<script>
import StdEdit from "./StdEdit.vue";

export default {
  components: {
    StdEdit,
  },
  props: {
    subjects: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      editingSubject: null,
    };
  },
  methods: {
    editSubject(index) {
      this.editingSubject = { ...this.subjects[index], index };
    },
    saveSubject(editedSubject) {
      this.$emit("save", editedSubject);
      this.cancelEdit();
    },
    deleteSubject(index) {
      this.$emit("delete", index);
    },
    cancelEdit() {
      this.editingSubject = null;
    },
  },
};
</script>

<style scoped>
.subject-table {
  width: 90%;
  margin: 20px auto;
  border-collapse: collapse;
  border: 1px solid #ccc; 
  border-radius: 5px; 
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); 
}

.subject-table th,
.subject-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
  font-size: 0.9em;
  font-weight: normal; 
}

.subject-table th {
  background-color: #a6caea; 
  text-transform: uppercase; 
  letter-spacing: 1px; 
}

.subject-table tbody tr:hover {
  background-color: #a6caea; 
}

.btn-sm {
  padding: 4px 8px;
  font-size: 0.8em;
  margin: 2px; 
}
</style>