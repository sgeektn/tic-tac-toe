<script setup>
  import {ref, onMounted} from 'vue'
  import BoardCase from './BoardCase.vue';
  const board = [];

  let end = false;
  const player = ref('x');
  const winner = ref('');
  
  init_board();

  function switch_player(){
    if (player.value == 'x'){
      player.value = 'o';
    }
    else
    {
      player.value = 'x';     
    }  
  };

  function handleClick(i,j){
    if (!end && board[i][j].value == "") { // and not end game
      board[i][j].value=player.value;
      switch_player();
      let win = check_winner();
    }
  };

  function check_line_or_col(index,is_line=true){
    let first = is_line ? board[index][0].value : board[0][index].value;
     
    if (first === '') {
      return null;
    }

    for (let i = 1; i < 3; i++) {
      const currentValue = is_line ? board[index][i].value : board[i][index].value;
      
      if (currentValue !== first || currentValue === '') {
        return null;
      }
    }

    return first;
  };

 
  function check_diag(is_reversed=false){
    let first = is_reversed ? board[0][2].value : board[0][0].value ;
     
    if (first === '') {
      return null;
    }

    for (let i = 1; i < 3; i++) {
      let counter = is_reversed ? (2 - i) : i;
      const currentValue = is_reversed ? board[i][counter].value : board[i][counter].value;
      
      if (currentValue !== first || currentValue === '') {
        return null;
      }
    }
    end = true;
    return first;
  };

 
  function check_winner(){
    end = false;
    let res = null;
    let i = 0;
    while (!end && i<3){
      res = check_line_or_col(i);
      if(!res){
        res = check_line_or_col(i,false);
      }
      i++;   
      end = !(res == null)
    }
    if(!res){
      res = check_diag();
    }
    if(!res){
      res = check_diag(true);
    }
    if (end)
    winner.value = "Player "+res+" Win";
  };

  function init_board(){
    winner.value= "";
    end = false;
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
    <h1>Current Player: {{ player }}</h1> 
    <table class="boardTable" border="1">
      <tr v-for="(item, index) in board">
        <td v-for="(boardCase, i) in item"> 
          <BoardCase :value=boardCase :i="index" :j="i" @handleClick="handleClick"></BoardCase>
        </td>
      </tr>
      
    </table>
    <h2>{{winner}}</h2>
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
