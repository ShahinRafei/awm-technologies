<script setup>
import { ref, watch, shallowRef, computed, reactive } from 'vue';

import WizardHeader from "./WizardsComponent/Header.vue";
import UserName from './WizardsComponent/UserName.vue';
import Email from './WizardsComponent/Email.vue';
import Review from './WizardsComponent/Review.vue';
import FormLayout from './WizardsComponent/FormLayout.vue';

const data = reactive({
    username: '',
    email: '',
});

const prevBtn = ref(false);
const nextBtn = ref(false);

const componentLevel = {
    1: UserName,
    2: Email,
    3: Review
}
const activeComponentLevel = ref(1);
const activeComponent = shallowRef(componentLevel[1]);

function getData(object){
    for(let key in object){
        data[key] = object[key];
    }
}

function goToNextForm() {
    if (activeComponentLevel.value < 3)
        activeComponentLevel.value++;
}

function goToPrevForm() {
    if (activeComponentLevel.value > 1)
        activeComponentLevel.value--;
}

function enableNextBtn(value) {
    nextBtn.value = Boolean(value);
}

function enablePrevBtn(){
    activeComponentLevel.value > 1 ? prevBtn.value = true : prevBtn.value = false;
}

watch(activeComponentLevel, () => {
    activeComponent.value = componentLevel[activeComponentLevel.value];
    enableNextBtn(false);
    enablePrevBtn();
});

const reviewData = computed(()=>{
    if(activeComponentLevel.value == 3)
        return data;
})

</script>

<template>
    <div class="container mx-auto py-10">
        <WizardHeader :level="activeComponentLevel" />
        <FormLayout>
            <keep-alive>
                <component :is="activeComponent" @nextComponent="goToNextForm" @prevComponent="goToPrevForm" @value="(object) => getData(object)" v-bind="reviewData"></component>
            </keep-alive>
        </FormLayout>
    </div>
</template>