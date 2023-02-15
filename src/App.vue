<template>
  <div class="app">
    <header>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order"></JobList>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Job from "./types/Job";
import OrderTerm from "./types/OrderTerm";
import JobList from "./components/JobList.vue";

export default defineComponent({
  name: "App",
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      { title: "FE", location: "seoul", salary: 1000000, id: "1" },
      { title: "BE", location: "jeju", salary: 2000000, id: "2" },
      { title: "Fullstack", location: "yongin", salary: 3000000, id: "3" },
      { title: "DBA", location: "seoul", salary: 4000000, id: "4" },
      { title: "PM", location: "incheon", salary: 5000000, id: "5" },
    ]);

    const order = ref<OrderTerm>("title");

    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return { jobs, handleClick, order };
  },
});
</script>

<style>
header {
  text-align: center;
}
header .order {
  margin-top: 20px;
}
button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
header .title {
  display: flex;
  justify-content: center;
}
header img {
  width: 60px;
  margin-right: 20px;
}
header h1 {
  font-size: 3em;
}
</style>
