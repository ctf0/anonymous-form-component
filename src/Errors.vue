<template>
    <transition name="slide-fade">
        <span class="help is-danger" v-if="errors" v-for="error in errors" dir="auto">
            {{ error }}
        </span>
    </transition>
</template>

<script>
export default {
    name: 'form-errors',
    props: ['errors']
}
</script>
