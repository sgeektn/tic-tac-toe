<script setup>
  import {ref ,defineProps} from 'vue'
  const props = defineProps(['value','player','i','j'])
  const emit = defineEmits(['handleClick'])
  const state = ref(props.value);

  
  function clicked(event){
    emit('handleClick',props.i,props.j);
  }
  
</script>

<template>
  <div class="boardCase" @click="clicked">   
    {{state}}
  </div>
</template>

<style scoped>
.boardCase {
  width: 40px;
  height: 40px;
  font-size: 65px;
  line-height: 30px;
  padding-left: 5px;

}
</style>
