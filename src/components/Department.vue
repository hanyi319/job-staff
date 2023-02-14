<template>
  <div class="wrapper">
    <div class="department">
      <div>
        <input type="checkbox" :id="departmentId" @click="selectDepartment" />
        <label for="department">部门 {{ departmentId }}</label>
      </div>
      <div>
        <button class="departmentButton" @click="toggleStaff">
          {{ toggleButton[staffVisible] }}
        </button>
      </div>
    </div>
    <div class="staff" v-if="staffVisible">
      <div class="staffBox">
        <input
          type="checkbox"
          :name="departmentId"
          :id="staffsIdMap[staffsId[0]]"
          @click="selectStaff"
        />
        <label :for="staffsIdMap[staffsId[0]]">小{{ staffsIdMap[staffsId[0]] }}</label>
      </div>
      <div class="staffBox">
        <input
          type="checkbox"
          :name="departmentId"
          :id="staffsIdMap[staffsId[1]]"
          @click="selectStaff"
        />
        <label :for="staffsIdMap[staffsId[1]]">小{{ staffsIdMap[staffsId[1]] }}</label>
      </div>
      <div class="staffBox">
        <input
          type="checkbox"
          :name="departmentId"
          :id="staffsIdMap[staffsId[2]]"
          @click="selectStaff"
        />
        <label :for="staffsIdMap[staffsId[2]]">小{{ staffsIdMap[staffsId[2]] }}</label>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Department",
  props: {
    departmentId: String,
    staffsId: Array,
  },
  setup(props, { emit }) {
    const staffsIdMap = {
      1: "一",
      2: "二",
      3: "三",
      4: "四",
      5: "五",
      6: "六",
      7: "七",
      8: "八",
      9: "九",
    };
    const toggleButton = {
      true: "+",
      false: "-",
    };
    const staffVisible = ref(true);
    const selectDepartment = () => {
      let department = document.getElementById(props.departmentId);
      let staffs = document.getElementsByName(props.departmentId);
      if (department.checked === true) {
        emit("selectDepartment", props.departmentId);
        for (let i = 0; i < staffs.length; i++) {
          staffs[i].checked = true;
        }
      } else {
        emit("unselectDepartment", props.departmentId);
        for (let i = 0; i < staffs.length; i++) {
          staffs[i].checked = false;
        }
      }
    };
    const selectStaff = (e) => {
      e.target.checked === true
        ? emit("selectStaff", e.target.id)
        : emit("unselectStaff", e.target.id);
      let department = document.getElementById(props.departmentId);
      let staffs = document.getElementsByName(props.departmentId);
      let staffsSelectedNumber = 0;
      for (let i = 0; i < staffs.length; i++) {
        staffs[i].checked === true ? (staffsSelectedNumber += 1) : (staffsSelectedNumber -= 1);
      }
      staffsSelectedNumber === 3 ? (department.checked = true) : (department.checked = false);
    };
    const toggleStaff = () => {
      staffVisible.value = !staffVisible.value;
      console.log(staffVisible.value);
      console.log(toggleButton[staffVisible.value]);
    };
    return {
      staffsIdMap,
      staffVisible,
      toggleButton,
      selectDepartment,
      selectStaff,
      toggleStaff,
    };
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.department {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  margin-bottom: 16px;
}

.departmentButton {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 1.5em;
  height: 1.5em;
  margin-left: 16px;
}

.staff {
  display: flex;
  margin-left: 16px;
  margin-bottom: 16px;
}

.staffBox {
  margin-right: 16px;
}
</style>
