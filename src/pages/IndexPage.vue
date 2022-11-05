<template>
  
 

  <div style="display:flex">
    <div style="margin-left:12%;margin-top:3%">
    <h4 class="text-blue" style="margin-left:0%;font-weight:600">HOTEL MANAGEMENT</h4>
    <h1 style="font-weight:500;margin-top:-5%">Your work</h1>
    <h1 style="font-weight:500;margin-left:5%;margin-top:-35%"><br/> — made</h1>
    <h1 style="font-weight:500;margin-top:-10%">&nbsp;Eazzzy.</h1>
  </div>    
    <img style="margin-left:10%;width:45%;height:25%;margin-top:7.5%" src="https://wallpapershome.com/images/pages/ico_h/19257.jpg"/>
      </div>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";

export default defineComponent({
  name: "IndexPage",
  setup() {
    return {
      slide: ref(1),
    };
  },
});
</script>
