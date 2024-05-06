<script setup>
//imports
import { defineProps, defineEmits } from 'vue';

//components
import Action from './Action.vue';

//emits
const emit = defineEmits(['nextComponent', 'prevComponent', 'value']);

//props
const props = defineProps(['email', 'username']);

//methods
function goToNextForm() {
    emit('nextComponent');
}

function goToPrevForm() {
    emit('prevComponent');
}

</script>
<template>
    <h2 class="text-center font-semibold text-slate-700">Step: review</h2>
    <ul class="self-start list-disc">
        <li>Username: {{ props.username }}</li>
        <li>Email: {{ props.email }}</li>
    </ul>
    <Action :prev="true" :next="false" @nextComponent="goToNextForm" @prevComponent="goToPrevForm"></Action>
</template>