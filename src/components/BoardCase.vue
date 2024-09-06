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
  width: 80px;
  height: 80px;
  font-size: 130px;
  line-height: 50px;
  padding-left: 10px;

}
</style>
