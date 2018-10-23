<template>
    <div class="alert" :class="'alert-' + type">
        <h2>{{ text }}</h2>
        <hr />
        <button 
                class="btn btn-success"
                @click="onNext()"
        >Next</button>
    </div>
</template>

<script>
import Vue from 'vue'
export default Vue.extend({
    props: ['type', 'text'],
    methods: {
        onNext(){
            this.$emit('onNext');
        }
    }
})
</script>

<style lang="scss" scoped>

</style>

