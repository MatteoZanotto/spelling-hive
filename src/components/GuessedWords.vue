<script setup lang="ts">
import { useGameStore } from '../stores/game';
import HiveButton from './HiveButton.vue';

const gameStore = useGameStore();

</script>

<template>
    <div class="container">
        <p v-if="!gameStore.victory">You have guessed {{ gameStore.guessedWords.length }} words. Still {{ gameStore.allowedWords.length - gameStore.guessedWords.length }} to find.</p>
        
        <div class="hint" v-if="!gameStore.victory">
            <HiveButton @click="gameStore.hint">Hint</HiveButton>
            <p>
                <span v-for="letter in [...gameStore.hintWord]" :class="{'highlight-letter': letter == gameStore.letters[3]}">
                    {{ letter.toUpperCase() + ' ' }}
                </span>
            </p>
        </div>
        
        <ul>
            <li v-for="word in gameStore.guessedWords">{{ word.toUpperCase() }}</li>
        </ul>
    </div>

    
    <!-- <div>
        <ul>
            <li v-for="word in gameStore.allowedWords">{{ word }}</li>
        </ul>
    </div>   -->
   

</template>

<style scoped>
.container {
    padding: 0 2rem;
}

ul {
  list-style-type: none;
  margin: 1rem 0;
  padding: 0;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

li {
    border-radius: 15%;
    border: 1px solid #cacaca;
    padding: 0.5rem 1rem;
    background-color: var(--gray);
}

.hint {
    display: flex;
    align-items: center;
    height: 2rem;
    gap: 2rem;
}

.highlight-letter {
    color: #ffdc42;
}
</style>