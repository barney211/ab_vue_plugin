<template>
  <div class="hello">
    <ab_select :selectedValue.sync="selectedValue5" placeholder="选择车辆" :width=210 :options="options"></ab_select>
    <div>从子组件传来的值: {{selectedValue5}}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      options:['你好吗','三山三闪闪山dddddddddddddddddddddddddddd','好了吗'],
      selectedValue5:'',
    }
  },
  methods:{
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
