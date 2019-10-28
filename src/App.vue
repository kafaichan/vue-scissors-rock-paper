<template>
  <div id="app">
      <div id="bot-placeholder">
        <img :src="bot_image" />        
      </div>
      <div id="you-placeholder">
        <img :src="you_image" />
      </div>
      <div id="buttons-container">
        <div @click="() => userPicked(1)" id="btn-paper"></div>
        <div @click="() => userPicked(2)" id="btn-scissor"></div>
        <div @click="() => userPicked(3)" id="btn-rock"></div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      botChoice: 0,
      userChoice: 0
    }
  },
  computed: {
    bot_image() {
      let botChoices = {};
      botChoices['-30'] = 'rock-lose.png';
      botChoices['-20'] = 'scissor-lose.png';
      botChoices['-10'] = 'paper-lose.png';
      botChoices['0'] = 'Placeholder-Bot.png';
      botChoices['10'] = 'paper-win.png';
      botChoices['20'] = 'scissor-win.png';
      botChoices['30'] = 'rock-win.png';
      botChoices['101'] = 'paper-draw.png';
      botChoices['102'] = 'scissor-draw.png';
      botChoices['103'] = 'rock-draw.png';
      return `/images/${botChoices[this.botChoice]}`
    },

    you_image() {
      let userChoices = {};
      userChoices['-30'] = 'rock-lose.png';
      userChoices['-20'] = 'scissor-lose.png';
      userChoices['-10'] = 'paper-lose.png';
      userChoices['0'] = 'Placeholder-You.png';
      userChoices['10'] = 'paper-win.png';
      userChoices['20'] = 'scissor-win.png';
      userChoices['30'] = 'rock-win.png';
      userChoices['101'] = 'paper-draw.png';
      userChoices['102'] = 'scissor-draw.png';
      userChoices['103'] = 'rock-draw.png';
      return `/images/${userChoices[this.userChoice]}`
    }
  },
  methods: {
    userPicked(user_pick) {      
      let bot_pick = Math.floor(Math.random() * 3 + 1);
      if(bot_pick == user_pick)
      {
        this.userChoice = user_pick + 100;
        this.botChoice = bot_pick + 100;
      }
      else if((user_pick==1 && bot_pick==3) || 
        (user_pick==2 && bot_pick == 1) || 
        (user_pick==3 && bot_pick == 2))
      {
        this.userChoice = user_pick * 10;
        this.botChoice = bot_pick * -10;
      }
      else if((user_pick==1 && bot_pick==2) || 
        (user_pick==2 && bot_pick == 3) || 
        (user_pick==3 && bot_pick == 1))
      {
        this.userChoice = user_pick * -10;
        this.botChoice = bot_pick * 10;
      }      
    }
  }
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background-color: #44D7B6;
  padding-top: 40px;
  box-sizing: border-box;
}

#bot-placeholder, #you-placeholder {
  flex: 0px 2 1;
}

#buttons-container {
  flex: 0px 1 1;
}

/*both margin left margin right set auto, the item will be centered*/
#bot-placeholder img, #you-placeholder img {
  display: block;
  width: 60%;
  height: auto;
  margin: auto;
}

#buttons-container {
  display: flex;
  flex-direction: row;
  flex: 0px 1 1;
}

#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}

#btn-paper {
  background-image: url("/images/paper-btn.png");
}

#btn-scissor {
  background-image: url("/images/scissor-btn.png");
}

#btn-rock {
  background-image: url("/images/rock-btn.png");
}
</style>
