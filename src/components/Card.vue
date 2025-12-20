<script setup>
    import IconFailSmall from '../icons/IconFailSmall.vue';
    import IconSuccesSmall from '../icons/IconSuccesSmall.vue';
    import IconFail from '../icons/IconFail.vue';
    import IconSucces from '../icons/IconSucces.vue';
    import { computed } from 'vue';

    const emit = defineEmits(['flip', 'answer']);

    const {word, translation, state, status} = defineProps({
        word: String,
        translation: String,
        state: String,
        status: String
    })

    const classState = computed(() => {
        return {
            turnClass: state === 'closed' ? 'card-turn' : 'card-turn none',
            iconsClass: state === 'opened' && status === 'pending' ? 'answer-icons' : 'answer-icons none',
            answerOptionClass: status === 'pending' && state === 'opened' ? 'stateAnswer none' : 'stateAnswer',
            completedClass: status === 'pending' ? 'completed none' : 'completed'
        }
    })

    const answerState = computed(() => {
        return {
            fail: status === 'fail' ? 'fail' : 'fail none',
            succes: status === 'succes' ? 'succes' : 'succes none'
        }
    })

    function handleFlip() {
        emit('flip');
    }

    function handleCorrect() {
        emit('answer', 'succes')
    }

    function handleWrong() {
        emit('answer', 'fail')
    }

</script>

<template>
    <div class="card">
        <div class="card-line"></div>
        <div class="card-line"></div>

        <div :class="classState.answerOptionClass">
            <div :class="answerState.fail">
                <IconFail/>
            </div>
            <div :class="answerState.succes">
                <IconSucces/>
            </div>
        </div>

        <div class="card-content">
            <div class="card-number">01</div>
            <div class="card-name">{{ word }}</div>

            <div :class="classState.turnClass" @click="handleFlip">Перевернуть</div>

            <div :class="classState.iconsClass">
                <div class="icon-fail" @click="handleWrong">
                    <IconFailSmall/>
                </div>
                <div class="icon-succes" @click="handleCorrect">
                    <IconSuccesSmall/>
                </div>
            </div>

            <div :class="classState.completedClass">Завершено</div>
        </div>
        
    </div>
</template>

<style scoped>
    .card {
        position: relative;
        overflow: hidden;

        background-color: var(--color-light);
        box-shadow: var(--box-shadow);
        border-radius: 16px;
        min-height: 376px;
        width: 100%;
        max-width: 250px;
        display: grid;
        padding: 28px 19px;
        transition: all .2s;
    }

    .completed {
        position: relative;
        text-transform: uppercase;
        font-weight: 600;
        z-index: 2;
    }

    .completed::before, .completed::after {
        content: '';
        position: absolute;
        width: 65px;
        height: 1px;
        background-color: var(--color-primary-accent);
        top: 50%;
        transform: translateY(-50%);
    }

    .completed::before {
        left: -70px;
        width: 70px;
    }

    .completed::after {
        right: -68px;

    }
    
    .stateAnswer {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        top: 20px;
        z-index: 3;

    }

    .fail, .succes {
        position: absolute;
        z-index: 2;
        left: 50%;
        transform: translateX(-50%);
    }

    .fail {
        top: -5px;
    }

    .answer-icons {
        position: absolute;
        display: flex;
        justify-content: space-between;
        align-items: center;
        column-gap: 32px;
        bottom: 22px;
    }

    .icon-fail, .icon-succes {
        position: relative;
        cursor: pointer;
    }

    .icon-fail::before, .icon-succes::after {
        content: '';
        position: absolute;
        width: 80px;
        height: 1px;
        background-color: var(--color-primary-accent);
        top: 50%;
        transform: translateY(-50%);
    }

    .icon-fail::before {
        left: -80px;
    }

    .icon-succes::after {
        right: -80px;
    }
    
    .card:hover {
        box-shadow: 10px 10px 10px 0px rgba(0, 0, 0, 0.05);
    }

    .card-content {
        display: grid;
        align-content: space-between;
        justify-items: center;
        margin-inline: auto;
        min-height: 320px;
        width: 100%;
        max-width: 212px;
    }

    .card-name {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
    }

    .card-line {
        content: '';
        position: absolute;
        background-color: var(--color-primary-accent);
        width: 1px;
        height: 355px;
        top: 50%;
        transform: translateY(-50%);
        border-radius: 4px;
        z-index: 1;
        pointer-events: none;
    }

    .card-line::after, .card-line::before {
        content: '';
        position: absolute;
        width: 8px;
        height: 8px;
        background-color: var(--color-primary-accent);
        border-radius: 50%;
    }

    .card-line::after {
        bottom: -4px;
    }

    .card-line::before {
        top: -4px;
    }

    .card-line:nth-child(1) {
        right: 20px;
        border-radius: 352px;
    }

    .card-line:nth-child(1)::after, .card-line:nth-child(1)::before {
        right: 0;
    }

    .card-line:nth-child(2) {
        left: 19px;
    }

    .card-turn {
        position: relative;
        width: 100%;
        text-align: center;
        cursor: pointer;
    }

    .card-turn::after, .card-turn::before {
        content: '';
        position: absolute;
        background-color: var(--color-primary-accent);
        top: 50%;
        transform: translateY(-50%);
        width: 20px;
        height: 1px;
        width: 66px;
    }

    .card-turn::before {
        left: -12px;
    }

    .card-turn::after {
        right: -12px;
    }

    .card-number {
        position: relative;
        width: 100%;
        text-align: start;
        padding-left: 16px;
    }

    .card-number::before, .card-number::after {
        content: '';
        background-color: var(--color-primary-accent);
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        height: 1px;
        width: 10px;
    }

    .card-number::before {
        left: -5px;
        width: 20px;
    }

    .card-number::after {
        width: 200px;
    }

    .none {
        display: none;
    }
</style>