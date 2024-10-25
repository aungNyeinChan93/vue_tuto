<template>

    <TodoList />
    <Onupdated_Moute/>

</template>

<script>

import Onupdated_Moute from "./components/Onupdated_Moute.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList,
    Onupdated_Moute,

  },
};
</script>
