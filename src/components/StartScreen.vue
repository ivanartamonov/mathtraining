<template>
    <div class="alert alert-secondary">
        <h2>Are you ready?</h2>
        <button class="btn btn-success" @click="$emit('onStart')">
            Start!
        </button>
    </div>
</template>

<script>
import Vue from 'vue'
export default Vue.extend({
    
})
</script>

<style lang="scss" scoped>
    .alert {
        text-align: center;
    }
    .btn {
        margin: 20px;
    }
</style>

