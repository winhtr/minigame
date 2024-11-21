<template>
<main-screen v-if="statusMatch === 'default'" @sendMatch="onHandleBeforeStart($event)"/>
<interact-screen-vue
  v-if="statusMatch === 'match'"
  :cardsContext="setting.cardContext" 
  @onFinish="onGetResult"/>
<result-screen-vue
  v-if="statusMatch === 'result'"
  :timer="timer" 
  @onStartAgain="statusMatch = 'default'"/>
<copy-right-screen/>
</template>

<script>
import CopyRightScreen from './components/CopyRightScreen.vue';
import InteractScreenVue from './components/InteractScreen.vue';
import MainScreen from './components/MainScreen.vue';
import ResultScreenVue from './components/ResultScreen.vue';

export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreenVue,
    ResultScreenVue,
    CopyRightScreen
  },
  data(){
    return{
      setting: {
        totalOfBlocks: 0,
        cardContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0
    }
  },

  methods: {
    onHandleBeforeStart(config){
      this.setting.totalOfBlocks = config.totalofBlock

      const firstCards = Array.from({ length: this.setting.totalOfBlocks / 2}, (_, i) => i + 1)
      const secondCards = [...firstCards]

      const cards = [...firstCards, ...secondCards];
      console.log('cards::', cards);

       function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]]; // Hoán đổi vị trí
            }
            return array;
        }

        this.setting.cardContext = shuffleArray(cards);

        console.log('Shuffled cards::', this.setting.cardContext);

        this.setting.startedAt = new Date().getTime();


      this.statusMatch = "match";
    },

    onGetResult() {      
      this.statusMatch = "result";

      this.timer = new Date().getTime() - this.settings.startedAt;
    }
}
}
</script>