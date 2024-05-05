<script setup>
import { reactive, defineEmits } from 'vue';
import { useVuelidate } from '@vuelidate/core';
import { required, helpers } from '@vuelidate/validators';

import Action from './Action.vue';

const state = reactive({
    userName: '',
})

const userNameRule = helpers.regex(/^[A-Za-z][A-Za-z0-9_]{5,20}$/);

const rules = {
    userName: {
        required: helpers.withMessage('Invalid Username.', required),
        userNameRule: helpers.withMessage('Invalid Username.', userNameRule)
    },
}

const v$ = useVuelidate(rules, state, { $autoDirty: true });

const emit = defineEmits(['nextComponent', 'value']);
function goToNextForm() {
    v$.value.$validate();
    if(!v$.value.$invalid){
        emit('nextComponent');
        emit('value', {username: state.userName});
    }
}

</script>

<template>
    <h2 class="text-center font-semibold text-slate-700">Username:</h2>
    <div>
        <input v-model="state.userName" type="text" id="username" name="username" class="border rounded-md px-5 py-2"
            placeholder="UserName">
        <p v-for="error of v$.userName.$errors" :key="error.$uid" class="text-xs font-bold text-red-400">
            {{ error.$message }}
        </p>
    </div>

    <Action :prev="false" :next="true" @nextComponent="goToNextForm" @prevComponent="$emit('prevComponent')">
    </Action>
</template>