<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>
          Topzee
        </ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding" :scrollY="false">

      <ion-card top-card>
        <ion-card-content top-content>
          <ion-img src="/assets/logo dice.png" style="height:100px;margin-bottom:10px"
            alt="topzee logo: two green dice"></ion-img>
          <ion-grid>
            <ion-row v-if="gameService.lifetimeStats.lastGame" bold>
              <ion-col>Last game</ion-col>
              <ion-col class="ion-text-end">{{ gameService.lifetimeStats.lastGame }}
              </ion-col>
            </ion-row>
            <ion-row>
              <ion-col>Games played</ion-col>
              <ion-col class="ion-text-end">{{ gameService.lifetimeStats.completedGameCount }}</ion-col>
            </ion-row>
            <ion-row>
              <ion-col>Average</ion-col>
              <ion-col class="ion-text-end">{{ gameService.lifetimeStats.averageScore }}</ion-col>
            </ion-row>
            <ion-row>
              <ion-col>High Score</ion-col>
              <ion-col class="ion-text-end">🏆 {{ gameService.lifetimeStats.highScore }}</ion-col>
            </ion-row>
          </ion-grid>
        </ion-card-content>
      </ion-card>

      <ion-button expand="block" v-if="!gameService.game?.playing" @click="playGame()">
        <ion-icon slot="start" :icon="add" color="success"></ion-icon>
        Start Game
      </ion-button>
      <ion-button expand="block" v-if="gameService.game?.playing" @click="playGame()">
        <ion-icon slot="start" :icon="pauseCircleOutline" color="success"></ion-icon>
        Resume Game ({{ gameService.game?.turnsLeft }} turns left)
      </ion-button>
      <ion-button expand="block" v-if="gameService.game?.playing" @click="restartGame()" color="light" fill="solid">
        Restart Game
      </ion-button>
      
    </ion-content>

  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, IonIcon, IonCard, IonCardContent, IonGrid, IonRow, IonCol, IonImg } from '@ionic/vue';
import { pauseCircleOutline, add } from 'ionicons/icons';
import { reactive } from 'vue';

const gameService = reactive({
  lifetimeStats: {
    lastGame: '2021-09-01',
    completedGameCount: 10,
    averageScore: 10.5,
    highScore: 20
  },
  game: {
    playing: false,
    turnsLeft: 3
  }
});

const playGame = () => {
  gameService.game.playing = true
}

const restartGame = () => {
  gameService.game.playing = false
}
</script>

<style scoped>
ion-card {
    margin: 0 0 16px;
    --color: black;
}

ion-button + ion-button {
    margin-top: 16px;
}

ion-card-content {
    padding: 12px;
    font-size: 2.5vh;
}

[bold] {
    font-weight: bold;
}
</style>
