<script setup>
//imports
import { defineProps } from "vue";

//props
const props = defineProps(['level']);
</script>

<template>
    <div class="w-full flex items-center">
        <!-- first item -->
        <div :class="['w-1/2 border-b', {'border-b-blue-500': props.level >= 1}]"></div>
        <div :class="['flex-shrink-0 w-20 !aspect-square flex justify-center items-center rounded-full border', {'border-blue-500 text-blue-500': props.level >= 1}]">1</div>
        <!-- end first item -->
        <!-- second item -->
        <div :class="['w-1/2 border-b', {'border-b-blue-500': props.level >= 2}]"></div>
        <div :class="['flex-shrink-0 w-20 !aspect-square flex justify-center items-center rounded-full border', {'border-blue-500 text-blue-500': props.level >= 2}]">2</div>
        <!-- end second item -->
        <!-- third item -->
        <div :class="['w-1/2 border-b', {'border-b-blue-500': props.level == 3}]"></div>
        <div :class="['flex-shrink-0 w-20 !aspect-square flex justify-center items-center rounded-full border',{'border-blue-500 text-blue-500': props.level == 3}]">3</div>
        <div :class="['w-1/2 border-b', {'border-b-blue-500': props.level == 3}]"></div>
        <!-- end third item -->
    </div>
</template>