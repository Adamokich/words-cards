<script setup>
    import { ref } from 'vue';
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';

    const score = ref(0);

    const card = ref({
        word: 'unadmitted',
        translation: 'Не осуществимый',
        state: 'closed',
        status: 'pending'
    })

    function flipWord() {
        card.value.word = card.value.translation;
        card.value.state = 'opened';
    }

    function getAnswer(answer) {
        card.value.status = answer;
    }

</script>

<template>
    <div class="content">
        <header class="header">
            <h1 class="header-title">Запомни слово</h1>
            <Score :score="score"/>
        </header>
        <Button/>
        <Card
        @flip="flipWord"
        @answer="getAnswer"
        v-bind="card"/>
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
</style>
