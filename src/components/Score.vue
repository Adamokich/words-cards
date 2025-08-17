<script setup>
    import IconScore from '../icons/IconScore.vue';

    const {score} = defineProps({
        score: Number,
    })

</script>

<template>
    <div class="score">
        <div class="score-stat">{{ score }}</div>
        <IconScore/>
    </div>
</template>

<style scoped>
    .score {
        display: flex;
        align-items: center;
        justify-content: center;
        column-gap: 10px;
        color: var(--color-primary);
        border-radius: 36px;
        background-color: var(--color-primary-accent);
        width: 100%;
        max-width: 110px;
        height: 48px;
    }
</style>