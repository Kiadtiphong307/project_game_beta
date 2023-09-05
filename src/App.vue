<script setup>
import { ref,} from 'vue'

const win_count_player1 = ref(0)
const draw_count_player1 = ref(0)
const loss_count_player1 = ref(0)

const win_count_player2 = ref(0)
const draw_count_player2 = ref(0)
const loss_count_player2 = ref(0)



const control_game = {
	'ค้อน': {
		'ค้อน': 'เสมอ',
		'กระดาษ': 'แพ้',
		'กรรไกร': 'ชนะ'
	},
	'กระดาษ': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'เสมอ',
		'กรรไกร': 'แพ้'
	},
	'กรรไกร': {
		'ค้อน': 'แพ้',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'เสมอ'
	}
}



const player1_choose = ref('');
const player2_choose = ref('');
const result = ref('');

const choiceImages = {
  'ค้อน': '/img/3.jfif',
  'กระดาษ': '/img/1.jfif',
  'กรรไกร': '/img/2.jfif',
};



function getRandomChoice() {
  const choices = ['ค้อน', 'กระดาษ', 'กรรไกร'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1_choose.value = getRandomChoice();
  player2_choose.value = getRandomChoice();

  const out_result = control_game[player1_choose.value][player2_choose.value];

  if (out_result === 'ชนะ') {
    win_count_player1.value++;
    loss_count_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_count_player2.value++;
    loss_count_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    draw_count_player1.value++;
    draw_count_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1_choose.value = '';
  player2_choose.value = '';
  result.value = '';
  win_count_player1.value = 0;
  draw_count_player1.value = 0;
  loss_count_player1.value = 0;
  win_count_player2.value = 0;
  draw_count_player2.value = 0;
  loss_count_player2.value = 0;
}

</script>

<template>
  <div class="contrainer_all">
    <div class="box_title">
			<div class="text_title">เกมเป่ายิ๊งฉุบ แสนสนุก </div>
      </div>

      <div class="contrainer_game">
        <div class="box_1" id="box_play1">
          Player 1 : ได้ออก {{ player1_choose }}
          <img v-if="player1_choose" :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img"/>
        </div>
        <div class="box_2" id="box_play2">
          Player 2 : ได้ออก {{ player2_choose }}
          <img v-if="player2_choose" :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />
        </div>
      </div>

    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> เป่ายิ๊งฉุบบบบบ </button>
    </div>

  <div class="contrainer_all_score"> 
    <div class="contrainer_score">
      <div class="box_score"> แต้มชนะ Player1 <br> {{ win_count_player1 }}  </div>  
      <div class="box_score"> แต้มแพ้ Player1 <br> {{ loss_count_player1 }} </div>
      <div class="box_score"> แต้มเสมอ Player1 <br>{{ draw_count_player1 }} </div>
    </div>
    <div class="contrainer_score">
      <div class="box_score"> แต้มชนะ Player2 <br> {{ win_count_player2 }}  </div>  
      <div class="box_score"> แต้มแพ้ Player2 <br> {{ loss_count_player2 }} </div>
      <div class="box_score"> แต้มเสมอ Player2 <br>{{ draw_count_player2 }} </div>
    </div>
  </div> 
    <div class="box_newgame">
      <button @click="reset_round" class="buttom_new"> เริ่มเกมใหม่ </button>
    </div>

  </div>    

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Itim&display=swap');


/*ALl body*/
:root {
  font-family: 'Itim', cursive;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: #242424;
  background-color: #ffffff;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  max-width: 1280px;
  margin:  auto;
  padding: 1rem;
  text-align: center;
}

*{
  padding: 10px;
}


/*background*/
.contrainer_all{
  background-image: linear-gradient( 135deg, #CE9FFC 10%, #7367F0 100%);
  border-radius: 50px;
}


.contrainer_game{
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin-left: 300px;
  margin-right: 250px;
  padding: 20px;
  justify-content: center;
}

.box_img {
  width: 100px;
  height: 100px; 
}


.contrainer_score{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.contrainer_all_score{
  border:2px solid black;
  border-radius: 50px;
  margin-left: 50px;
  margin-right: 50px;
}


.text_title{
  background-image: linear-gradient( 135deg, #FCCF31 10%, #F55555 100%);
  width: 500px;
  height: 70px;
  border-radius: 50px;
  margin: auto; 
  display: flex;
  align-items: center;
  justify-content: center;  
  font-size: 32px;

}


.buttom_new{
  padding: 20px;
  width: 7rem;
  height: 2.5rem;
  background-color: red;
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.buttom_start:hover{
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  0 3px 6px rgb(0, 0, 0.23);
  transform:translate(0px, -8px) ;
  transition: 0.4s;
  padding: 15px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
  color: white;
}


.buttom_start{
  padding: 20px;
  width: 9rem;
  height: 2.5rem;
  background-image: linear-gradient( 135deg, #81FBB8 10%, #28C76F 100%);
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.box_newgame,.start_buttom{
  display: flex;
  justify-content: center;
  align-items: center; 
  margin-top: 20px;
}

</style>