<script setup>
import Department from "./components/Department.vue";
import { ref } from "vue";
const department = ref([]);
const pushDepartmentArray = (departmentId) => {
  department.value.push(departmentId);
};
const popDepartmentArray = (departmentId) => {
  department.value.pop(departmentId);
};
const staff = ref([]);
const pushStaffArray = (staffId) => {
  staff.value.push(staffId);
};
const popStaffArray = (staffId) => {
  staff.value.pop(staffId);
};
</script>

<template>
  <div class="wrapper">
    <span class="title">请选择部门 / 员工：</span>
    <Department
      departmentId="1"
      :staffsId="[1, 2, 3]"
      @selectDepartment="pushDepartmentArray"
      @unselectDepartment="popDepartmentArray"
      @selectStaff="pushStaffArray"
      @unselectStaff="popStaffArray"
    />
    <Department
      departmentId="2"
      :staffsId="[4, 5, 6]"
      @selectDepartment="pushDepartmentArray"
      @unselectDepartment="popDepartmentArray"
      @selectStaff="pushStaffArray"
      @unselectStaff="popStaffArray"
    />
    <Department
      departmentId="3"
      :staffsId="[7, 8, 9]"
      @selectDepartment="pushDepartmentArray"
      @unselectDepartment="popDepartmentArray"
      @selectStaff="pushStaffArray"
      @unselectStaff="popStaffArray"
    />
    <span class="title">选中结果：</span>
    <span>{"department":{{ department }}, "user":{{ staff }}}</span>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 50vw;
}

.title {
  margin: 16px 0;
}
</style>
