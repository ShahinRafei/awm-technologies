<script setup>
//imports
import {defineProps} from 'vue';

//components
import Action from './Action.vue';

//props
const props = defineProps(['email', 'username']);

</script>
<template>
    <h2 class="text-center font-semibold text-slate-700">Step: review</h2>
    <ul class="self-start list-disc">
        <li>Username: {{ props.username }}</li>
        <li>Email: {{ props.email }}</li>
    </ul>
    <Action :prev="true" :next="false" @nextComponent="$emit('nextComponent')" @prevComponent="$emit('prevComponent')"></Action>
</template>