<template lang="html">
  <div class="">
    <div class="" v-for="list in lists">
      {{list.name}}
    </div>
    name : <input type="text" name="name" value="" v-model="name">
    phone : <input type="text" name="name" value="" v-model="phone">
    <button type="button" name="button" @click="add(name, phone)">Submit</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      lists: [],
      name: '',
      phone: ''
    }
  },
  computed: {},
  mounted () {
    this.getData()
    var vm = this
    setInterval(function () {
      vm.getData()
    }, 3000)
  },
  methods: {
    getData: function () {
      let vm = this
      this.$http.get('http://localhost:3000/data').then(function (res) {
        vm.lists = res.data
      })
    },
    add (name, phone) {
      let data = {
        name,
        phone
      }
      console.log(data)
      this.$http.post('http://localhost:3000/data', data).then(function (res) {
        console.log(res)
      })
    }
  },
  components: {}
}
</script>

<style lang="css">
</style>
