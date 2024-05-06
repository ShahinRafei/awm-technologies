<script setup>
//imports
import { ref, watch, shallowRef, computed, reactive } from 'vue';

//conponents
import WizardHeader from "./WizardsComponent/Header.vue";
import UserName from './WizardsComponent/UserName.vue';
import Email from './WizardsComponent/Email.vue';
import Review from './WizardsComponent/Review.vue';
import FormLayout from './WizardsComponent/FormLayout.vue';

//data
const data = reactive({
    username: '',
    email: '',
});

const componentLevel = {
    1: UserName,
    2: Email,
    3: Review
}
const activeComponentLevel = ref(1);
const activeComponent = shallowRef(componentLevel[1]);

//methods

//this method is for get email and username from different components
function getData(object){
    for(let key in object){
        data[key] = object[key];
    }
}

//this method is for navigate and go to next input
function goToNextForm() {
    if (activeComponentLevel.value < 3)
        activeComponentLevel.value++;
}

//this method is for navigate and go to previous input
function goToPrevForm() {
    if (activeComponentLevel.value > 1)
        activeComponentLevel.value--;
}

//watchers

//change components dynamically
watch(activeComponentLevel, () => {
    activeComponent.value = componentLevel[activeComponentLevel.value];
});

//computed

//to send email and username to review component
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