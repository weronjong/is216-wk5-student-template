<script setup>
import { ref, computed } from 'vue'

const teamA = ref("Falcons")
const teamB = ref("Tigers")
const scoreA = ref(0)
const scoreB = ref(0)
const step = ref(1) // points added per click
const maxScore = ref(10)

function addA() {
    scoreA.value = Math.min(maxScore.value, scoreA.value + step.value);
}

function addB() {
    scoreB.value = Math.min(maxScore.value, scoreB.value + step.value);
}

function reset() {
    scoreA.value = 0;
    scoreB.value = 0;
}

const total = computed(() => scoreA.value + scoreB.value)
const pointsLeftA = computed(() => maxScore.value - scoreA.value)
const pointsLeftB = computed(() => maxScore.value - scoreB.value)

const status = computed(() => {
    if (scoreA.value === maxScore.value && scoreB.value === maxScore.value) {
        return `${teamA.value} and ${teamB.value} are tied!`
    }
    if (scoreA.value === maxScore.value) return `${teamA.value} wins!`
    if (scoreB.value === maxScore.value) return `${teamB.value} wins!`
    return 'Game in progress...'
})

</script>

<template>

    <div style="font-family: Arial; max-width: 520px; margin: 24px auto;">
        <h2>Mini Scoreboard</h2>

        <p><strong>{{ teamA }}</strong> vs <strong>{{ teamB }}</strong></p>

        <p>Current: {{ scoreA }} - {{ scoreB }}</p>

        <p>Total: {{ total }}</p>
        <p>{{ teamA }} points left: {{ pointsLeftA }}</p>
        <p>{{ teamB }} points left: {{ pointsLeftB }}</p>

        <div style="display: flex; gap: 12px; margin: 12px 0;">
            <button @click="addA">+ Team A</button>
            <button @click="addB">+ Team B</button>
            <button @click="reset">Reset</button>
        </div>


        <div style="margin-top: 14px;">
            <strong>{{ status }}</strong>
        </div>


    </div>

</template>

<style scoped>
p,
input {
    font-family: monospace;
}

p {
    white-space: pre;
}
</style>
