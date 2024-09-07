<script setup>
  import {ref ,defineProps} from 'vue'
  const props = defineProps(['value','player','i','j'])
  const emit = defineEmits(['handleClick'])
  const state = ref(props.value);
  function color( ){
    if(state.value=='x'){
      return  { 'color': 'black'};
    }else if(state.value=='o'){
      return  { 'color': 'red'};
    }
  };

  function clicked(event){
    emit('handleClick',props.i,props.j);
  }

</script>

<template>
  <div class="boardCase" @click="clicked" :style="color()" >   
    {{state}}
  </div>
</template>

<style scoped>

.boardCase {
  width: 25vw;
  height: 25vw;
  font-size: 40vw;
  line-height: 15vw;
  padding-left: 10px;

}

@media screen  and (min-width: 800px) {
  .boardCase {
    width: 10vw;
    height: 10vw;
    line-height: 8vw;
    font-size: 25vw;
    padding-left: 1vw;

}
}
</style>
