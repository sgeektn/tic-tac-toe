<script setup>
  import {ref, onMounted} from 'vue'
  import BoardCase from './BoardCase.vue';
  const board = [];
  init_board();
  const player = ref('x');




  function switch_player(){
    if (player.value == 'x'){
      player.value = 'o';
    }
    else
    {
      player.value = 'x';     
    }  
  };

  function test(i,j){
    if (board[i][j].value == "") {
      board[i][j].value=player.value;
      switch_player();
      console.log(board.value);
      console.log(player.value);
    }
  };

  function init_board(){
    console.log('init_board');
    for(let i=0;i<3;i++){
      if(board[i] == null)
        board[i]=[];
        for(let j=0;j<3;j++){
          if(board[i][j]==null){
            board[i][j]=ref('');
          }
          else{
            board[i][j].value='';}
          }
    }
  }
</script>

<template>
  <div class="board">
    <h1>Player: {{ player }}</h1> 
    <table class="boardTable" border="1">
      <tr v-for="(item, index) in board">
        <td v-for="(boardCase, i) in item"> 
          <BoardCase :value=boardCase :i="index" :j="i" @handleClick="test"></BoardCase>
        </td>
      </tr>
      
    </table>
    <button @click="init_board">Replay</button>
  </div>
</template>

<style scoped>
table {
  border-collapse: collapse;
  border: none;
}

.boardTable td {
  border: 2px solid black;
}

.boardTable tr:first-child td {
  border-top: none;
}

.boardTable tr:last-child td {
  border-bottom: none;
}

.boardTable tr td:first-child {
  border-left: none;
}

.boardTable tr td:last-child {
  border-right: none;
}
</style>
