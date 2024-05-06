<script setup>
//imports
import { reactive } from 'vue';
import { useVuelidate } from '@vuelidate/core';
import { required, helpers, email } from '@vuelidate/validators';

//components
import Action from './Action.vue';

//data
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

//emit navigate and email data
const emit = defineEmits(['nextComponent', 'prevComponent', 'value']);


//methods
//check email validation
function goToNextForm() {
    v$.value.$validate();
    if(!v$.value.$invalid){
        emit('nextComponent');
        emit('value', {email: state.email});
    }
}

function goToPrevForm() {
    emit('prevComponent');
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
    <Action :prev="true" :next="email" @nextComponent="goToNextForm" @prevComponent="goToPrevForm"></Action>
</template>