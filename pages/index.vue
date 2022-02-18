<template>
  <div>
    <div>TOTAL: {{categories.length}}</div>
    <v-text-field v-model="filterVal" style="max-width: 300px;" outlined dense filter></v-text-field>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">Categories</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(el,i) in categories" :key="i">
            <td>{{ el }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      count: 0,
      categoriesVal: [],
      filterVal: ""
    }
  },
  async created () {
    const categoriesObject = await this.$axios.$get('https://api.publicapis.org/categories')
    this.categoriesVal = categoriesObject.categories
    this.count = categoriesObject.count
  },
  computed: {
    categories() {
      return this.categoriesVal.filter((category) => {
        if(category.toLowerCase().includes(this.filterVal.toLowerCase())) {
          return category
        }
      })

    }
  }
};
</script>
