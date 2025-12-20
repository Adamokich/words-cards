<script setup>
    import { computed, isRef, nextTick, onMounted, ref } from 'vue';
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';

    const API_ENDPOINT = 'http://localhost:8080/api/random-words';

    let score = ref(0);
    let cardsData = ref([]);

    onMounted(() => {
        getCards();
    })
    

    async function getCards() {
        const res = await fetch(`${API_ENDPOINT}`);

        cardsData.value = await res.json();

        cardsData.value = cardsData.value.map(item => ({...item, state: 'closed', status: 'pending'}));
    }

     const cards = computed(() => cardsData.value);
    
    function flipWord(word) {
        const card = cardsData.value.find(item => item.word === word);
        if (card) {
            card.state = 'opened';
            card.word = card.translation;
        }
    }

    function handleAnswer(word, answer) {
        const card = cardsData.value.find(item => item.word === word);
        if (card) card.status = answer;
    }
    
</script>

<template>
    <div class="content">
        <header class="header">
            <h1 class="header-title">Запомни слово</h1>
            <Score :score="score"/>
        </header>
        <Button/>
        <div class="cards">
            <Card 
            v-for="item in cards"
            :key="item.word"
            :word="item.word"
            :translation="item.translation"
            :state="item.state"
            :status="item.status"
            @flip="flipWord"
            @answer="handleAnswer"
            />
        </div>
    </div>
</template>

<style scoped>
    .content {
        display: grid;
        align-content: space-between;
        height: 100%;
    }

    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .header-title {
        font-size: 16px;
    }

    .cards {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        row-gap: 20px;
    }
</style>
