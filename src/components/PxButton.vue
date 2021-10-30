<template>
    <button
        @click="buttonClick"
        class="bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-2 border border-red-500 hover:border-transparent rounded">
        <beat-loader
            :loading="isLoading"
            color="#68d391"
            :size="8"
        />
        <slot v-if="!isLoading">
        </slot>
    </button>
</template>

<script>
export default {
    name : 'PxButton',
    props: {
        isLoading:{
            type:Boolean,
            default:false,
        }
    },
    methods:{
        buttonClick(){
            // alert("this.$emit('custom-click')");
            this.$emit('custom-click')
        }
    }
}
</script>
