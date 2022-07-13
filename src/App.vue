<template>
  <div class="app">
     <IndexComponent></IndexComponent>
  <ListComponent></ListComponent>
  <WeeklyComponent></WeeklyComponent>
  <MondayComponent></MondayComponent>
  
  </div>
 
</template>

<script>
import IndexComponent from './components/IndexComponent.vue'
import WeeklyComponent from './components/WeeklyComponent.vue'
import ListComponent from './components/ListComponent.vue'
import MondayComponent from './components/MondayComponent.vue'



export default {
  name: 'App',
  components: {
    IndexComponent,
    WeeklyComponent,
    ListComponent,
    MondayComponent
}
}
</script>

<style>
@import "@/assets/css/bodyestile.css";
</style>
