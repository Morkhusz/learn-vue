<template>
  <div id="app">

    <label>Lista</label>
    <br />
    <input @click="show = !show" v-model="filter" type="text" />
    <div v-show="show" style="background-color: grey; margin: 0 auto; width: 20%">
      <div
        v-for="(value, index) in list"
        :key="value"
        @click="select(index, $event)"
      >
        {{ value }}
      </div>
    </div>

    <div style="margin-top: 30%">
      selecionados
      <pre>
        {{ selectedValues }}
      </pre>
    </div>

  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    //
  },
  data: () => {
    return {
      show: false,
      selectedValues: [],
      values: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      filter: "",
      name: "",
    };
  },
  computed: {
    list() {
      if (this.filter !== "") {
        return this.values.filter((e) => e.toString().includes(this.filter));
      }

      return this.values;
    },
  },
  methods: {
    select(index, e) {
      let selected = this.list[index];
      let selectedIndex = this.selectedValues.indexOf(selected);
      if (selectedIndex > -1) {
        e.target.style.backgroundColor = "grey";
        this.selectedValues.splice(selectedIndex, 1);

        return;
      }
      this.selectedValues.push(selected);
      e.target.style.backgroundColor = "green";
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
