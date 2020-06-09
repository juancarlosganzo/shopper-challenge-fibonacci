<template>
  <div id="app">
      <b-container>
          <br />
        <Fibonacci />
      </b-container>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import Fibonacci from './components/Fibonacci.vue'


var data = { 
  limite: "",
  result : 0,
   }
export default {
  name: 'App',
  data:function(){
    return data;
  },
  components: {
    Fibonacci
  },computed: {

  },methods:{
    
  }
}
</script>


