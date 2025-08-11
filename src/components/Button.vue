<script setup></script>

<template>
    <button class="button">Начать игру</button>
</template>

<style scoped>
    .button {
        cursor: pointer;
        border: none;
        font-size: 24px;
        color: var(--color-light);
        border-radius: 100px;
        background-color: var(--color-primary);
        padding: 16px;
        transition: all .3s;
        max-width: 100%;
        width: 335px;
        min-height: 68px;
    }

    .button:hover {
        background-color: var(--color-primary-inverted);
    }
</style>