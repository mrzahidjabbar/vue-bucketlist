<template>
  <div>
    <h1>{{ msg }}</h1>
    <p>Here you can manage your daily activites</p>
    <div class="container col-sm-12 col-md-8 col-lg-6 mt-5 justify-content-center">
      <b-row class="justify-content-center">
        <b-input-group class="shadow" prepend="Item">
          <b-form-input
            v-model="task"
            @keyup.enter="addItem"
            range="true"
            type="text"
            placeholder="Enter here"
          ></b-form-input>
          <b-input-group-append>
            <date-picker
              v-model="date"
              lang="eng"
              format="YYYY-MM-DD"
              value-type="date"
              type="date"
            ></date-picker>
            <b-button @click="addItem" variant="info">+</b-button>
          </b-input-group-append>
        </b-input-group>
      </b-row>
      <div class="container mt-4">
        <b-row
          class="items mb-1 justify-content-center shadow"
          v-for="(item,index) in tasks"
          :key="{index}"
        >
          <div class="w-100 d-flex justify-content-between">
            <div>
              <div class="ml-3 p-2">
                <span v-if="item.dueDate" class="item--date">{{item.dueDate.toDateString()}}</span>
                <span v-else class="item--date">No Due Date</span>
                <span>{{item.dueTask}}</span>
              </div>
            </div>
            <div>
              <b-button @click="removeItem(index)" class="rounded p-2" variant="primary">Remove</b-button>
            </div>
          </div>
        </b-row>
      </div>
    </div>
  </div>
</template>

<script>
import DatePicker from "vue2-datepicker";
export default {
  components: {
    DatePicker
  },
  name: "ToDo",
  props: {
    msg: String
  },
  // data for app
  data() {
    return {
      id: 0,
      task: "",
      tasks: [],
      date: ""
    };
  },

  methods: {
    //method for adding item
    addItem() {
      if (this.task) {
        this.tasks.push({
          dueTask: this.task,
          dueDate: this.date
        });
      } else {
        alert("Enter Item");
      }
      this.task = "";
      this.date = "";
    },
    //method for removing item
    removeItem(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<!-- Custom Scoped Styles -->
<style scoped>
.row {
  margin-right: 0;
  margin-left: 0;
}
.bg-success {
  background-color: #d9e75d !important;
}
.item--date {
  margin-right: 50px;
  color: rgb(77, 9, 145);
  border-bottom: 1px dotted rgb(77, 9, 145);
  background-color: rgb(230, 247, 156);
}
.mx-datepicker {
  max-width: 118px;
}
</style>
<!--Custom styles -->
<style >
.mx-input-wrapper {
  height: 100%;
}
.mx-input {
  width: 100%;
  height: 100% !important;
  border-radius: 0px !important;
}
</style>
