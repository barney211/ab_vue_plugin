<template>
    <div>
      <div style="position:relative;height:42px;">
        <div :style="{border:'1px solid '+borderColor,display: 'flex',width:width+'px'}">
          <input class="ab_input" type="text" @input="inputValue" @focus="focusOnInput" v-model="sValue" :placeholder="placeholder" :style="{width: (width-36)+'px',background:background,color:color}">
          <div class="click_icon" @click="showPop=!showPop"  :style="{border:iconBorder,background:iconBackground}">
            <img class="iconImg" v-if="showPop" src="./arrowUp.png" alt="">
            <img class="iconImg" v-else src="./arrowDown.png" alt="">
          </div>
        </div>
        <div class="pop_window" v-if="showPop" :style="{background:popBackground,border: '1px solid'+ popBorderColor,minWidth:width+'px'}">
          <div class="pop_item" v-for="item,index in optionsForSelect" :style="{borderBottom:index<options.length-1?'1px solid'+popSepLine:'none'}" @click="chooseItem(item)">{{item}}</div>
          <!--下拉框的三角-->
          <div class="triangleIcon" :style="{borderColor: 'transparent '+popBorderColor+' transparent transparent'}"></div>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "ab_select",
        props: {
          selectedValue:{
            type:String,
            default:'',
          },
          options:{
            type:Array,
            default:[],
          },
          placeholder:{
            type: String,
            default:'请选择'
          },
           width: {
              type: Number,
              default: 210,
           },
           background:{
              type: String,
              default:'#050b1c'
           },
           borderColor:{
             type:String,
             default:'#202949'
           },
           color:{
              type:String,
              default:'#848ca3'
           },
          iconBackground:{
            type:String,
            default:'#050b1c'
          },
          iconBorder:{
            type:String,
            default:'none'
          },
          popBackground:{
            type:String,
            default:'#020a1f'
          },
          popBorderColor:{
            type:String,
            default:'#006062'
          },
          popSepLine:{
            type:String,
            default:' #282e3d'
          }

        //props结尾
      },
        data() {
            return {
              showPop:false,
              sValue:'',
              optionsForSelect:[],
            }
        },
        methods: {
          chooseItem(item){
            var vm=this;
            vm.sValue=item;
            vm.showPop=false;
            vm.optionsForSelect=vm.options;
          },
          focusOnInput(){
            var vm=this;
            vm.showPop=true;
          },
          inputValue(){
            var vm=this;
            vm.optionsForSelect=[];
            for(var i=0;i<vm.options.length;i++){
               if(vm.options[i].indexOf(vm.sValue)!=-1){
                 vm.optionsForSelect.push(vm.options[i])
               }
            }
            if(vm.optionsForSelect.length<1){
              vm.optionsForSelect.push('')
            }
          },
        },
        watch:{
          sValue(){
            var vm=this;
            vm.$emit('update:selectedValue',vm.sValue)
          },
        },
        components: {},
        mounted() {
          var vm=this;
          vm.optionsForSelect=vm.options;
        },
        destroyed() {
        }
    }
</script>

<style scoped>
  *{
    box-sizing: border-box;
  }
   .ab_input{
     padding-left: 10px;padding-right: 10px;
     height:36px;
     outline: none;
     border: none;
   }
  .pop_window{
    z-index:10000000;padding-left: 10px;padding-right: 10px;position: absolute;top:46px;left:0;border-radius: 3px;
  }
  .click_icon{
    display: flex;align-items: center;width:36px;height:36px;
  }
  .pop_item{
    textAlign:center;height:39px;
    line-height: 39px;
  }
  .iconImg{
    margin-left: 10px;
  }
  .pop_item:hover{
    color:#00ffff;
  }
  /*自己写三角 下*/
  .triangleIcon{
    position: absolute;
    top:-16px;
    left:15px;
    width: 0;
    height: 0;
    border-width: 8px;
    border-style: solid;
    transform: rotate(90deg); /*顺时针旋转90°*/
  }
  /*自己写三角 上*/
</style>
