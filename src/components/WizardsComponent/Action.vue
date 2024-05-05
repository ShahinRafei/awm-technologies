<script setup>
//imports
import { defineProps } from 'vue';

//props
const props = defineProps(['prev', 'next']);

</script>
<template>
    <div class="w-full flex justify-between items-center">
        <!-- prev btn -->
        <button @click="$emit('prevComponent')" id="btn-prev" class="px-5 py-2 bg-teal-600 rounded-md text-white font-semibold shadow-md hover:bg-slate-600 disabled:opacity-50 disabled:bg-slate-600" :disabled="!props.prev">
            Prev
        </button>
        <!-- end prev btn -->
        <!-- next btn -->
        <button @click="$emit('nextComponent')" id="btn-next" class="px-5 py-2 bg-teal-600 rounded-md text-white font-semibold shadow-md hover:bg-slate-600 disabled:opacity-50 disabled:bg-slate-600" :disabled="!props.next">
            Next
        </button>
        <!-- end next btn -->
    </div>
</template>