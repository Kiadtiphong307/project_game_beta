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
  'ค้อน': '/img/3.png',
  'กระดาษ': '/img/1.png',
  'กรรไกร': '/img/2.png',
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

