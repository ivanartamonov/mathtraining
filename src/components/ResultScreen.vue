<template>
    <div class="alert alert-secondary">
        <h2>Done!</h2>
        <hr />
        <p>Success: {{ stats.success }}</p>
        <p>Fail: {{ stats.error }}</p>
        <button class="btn btn-success" @click="onStartNewGame()">START NEW GAME</button>
    </div>
</template>

<script>
export default {
    props: ['stats'],
    methods: {
        onStartNewGame() {
            this.$emit('onStartNewGame');
        }
    }
}
</script>

<style lang="scss" scoped>

</style>

