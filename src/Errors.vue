<template>
    <transition name="slide-fade">
        <span class="help is-danger" v-if="errors" v-for="error in errors" dir="auto">
            {{ error }}
        </span>
    </transition>
</template>

<style scoped>
    /*animation*/
    .slide-fade-enter-active,
    .slide-fade-leave-active {
        transition: all 0.3s ease;
    }
    .slide-fade-enter,
    .slide-fade-leave-to {
        opacity: 0;
        transform: translateX(10px);
    }
</style>

<script>
export default {
    name: 'form-errors',
    props: ['errors']
}
</script>
