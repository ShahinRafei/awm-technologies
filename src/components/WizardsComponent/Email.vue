<script setup>
import { reactive } from 'vue';
import { useVuelidate } from '@vuelidate/core';
import { required, helpers, email } from '@vuelidate/validators';

import Action from './Action.vue';

const state = reactive({
    email: '',
})

const rules = {
    email: {
        required: helpers.withMessage('Invalid email address.', required),
        email: helpers.withMessage('Invalid email address.', email),
    },
}

const v$ = useVuelidate(rules, state, { $autoDirty: true });

const emit = defineEmits(['nextComponent', 'value']);

function goToNextForm() {
    v$.value.$validate();
    if(!v$.value.$invalid){
        emit('nextComponent');
        emit('value', {email: state.email});
    }
}

</script>
<template>
    <h2 class="text-center font-semibold text-slate-700">Email:</h2>
    <div>
        <input v-model="state.email" type="text" id="email" name="email" class="border rounded-md px-5 py-2" placeholder="Email">
        <p v-for="error of v$.email.$errors" :key="error.$uid" class="text-xs font-bold text-red-400">
            {{ error.$message }}
        </p>
    </div>
    <Action :prev="true" :next="email" @nextComponent="goToNextForm" @prevComponent="$emit('prevComponent')"></Action>
</template>