<template>
  <q-layout view="lHh Lpr lFf">
  <div style="display:flex;">
    <div style="margin-top:-2%;margin-left:5.5%">
           <h5><a href="/#/" style="text-decoration: none;" class=" text-black">H & M </a></h5>
          </div>     
           <div style="display:flex;margin-top:-2%;margin-left:75%">
          <h6 style="display:flex"><a href="/#/hotels" style="text-decoration: none" class="text-black">Hotels</a></h6>
          &nbsp;&nbsp;&nbsp;
         <h6> <a href="/#/rooms" style="text-decoration: none" class="text-black">Rooms</a>
        </h6>
      </div>
      </div>


<!-- <div style="display:flex">
  <div style="margin-left:10%;margin-top:3%">
  <h4 class="text-blue" style="margin-left:0%;font-weight:600">HOTEL MANAGEMENT</h4>
  <h1 style="font-weight:bold;margin-top:-5%">Your work</h1>
  <h1 style="font-weight:bold;margin-left:5%;margin-top:-35%"><br/> — made</h1>
  <h1 style="font-weight:bold;margin-top:-10%">&nbsp;Eazzzy.</h1>
</div>    
  <img style="margin-left:10%;width:40%;height:10%;margin-top:8%" src="https://wallpapershome.com/images/pages/ico_h/19257.jpg"/>
    </div> -->

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";

const linksList = [
  {
    title: "Hotels",
    caption: "Hotels",
    icon: "hotels",
    link: "/#hotels",
  },
  {
    title: "Rooms",
    caption: "Rooms",
    icon: "room",
    link: "/#rooms",
  },
];

export default defineComponent({
  name: "MainLayout",

  // components: {
  //   EssentialLink,
  // },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
