<script setup>
    import Button from './components/Button.vue';
    import Score from './components/Score.vue';
    import Card from './components/Card.vue';
    
    let isFlipped = true;
    let answerVariable = false;
    let completed = true;

    const eng = 'unadmitted';
    const rus = 'Не осуществимый';

    const score = 50;

    function handleFlip() {
        isFlipped = !isFlipped;
    }

    function handleAnswer(answer) {
       answer ? answerVariable = true: answerVariable = false;
       completed = true;
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
        @flip="handleFlip"
        @answer="handleAnswer"
        :answer="answerVariable"
        :word="isFlipped ? rus : eng"
        :isFlipped="isFlipped"
        :completed="completed"/>
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
