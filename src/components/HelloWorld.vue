<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ status }}</h2>
    <h3>Users</h3>
    <ul>
      <li v-for="user in users" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data: function () {
    return {
      users: [],
    };
  },
  beforeCreate: function () {
    console.count("beforeCreate");
  },
  created: async function () {
    console.count("create");
    const data = await this.getUsers();
    // https://vuejs.org/v2/guide/reactivity.html#For-Arrays
    // https://medium.com/@miladmeidanshahi/update-array-and-object-in-vuejs-a283983fe5ba
    this.users.splice(0, this.users.length);
    this.users.push(...data);
  },
  beforeMount: function () {
    console.count("beforeMount");
  },
  mounted: function () {
    console.count("mounted");
    console.log(this);
  },
  beforeUpdate: function () {
    console.count("beforeUpdate");
  },
  updated: function () {
    console.count("mounted");
  },
  activated: function () {
    console.count("activated");
  },
  deactivated: function () {
    console.count("mounted");
  },
  beforeUnmount: function () {
    console.count("beforeUnmount");
  },
  unmounted: function () {
    console.count("unmounted");
  },
  errorCaptured: function () {
    console.count("errorCaptured");
  },
  renderTracked: function () {
    console.count("renderTracked");
  },
  renderTriggered: function () {
    console.count("renderTriggered");
  },
  methods: {
    async getUsers() {
      // https://jsonplaceholder.typicode.com/
      // const url = "https://jsonplaceholder.typicode.com/users";
      const url = "http://localhost:3000/users";
      const promised = await fetch(url);
      const data = await promised.json();
      return data;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
