<template>
    <div class="alert alert-secondary">
        <h2>{{ x }} + {{ y }} = ?</h2>
        <hr />
        <div class=buttons>
            <button 
                class="btn btn-success" 
                v-for="number in answers"
                v-bind:key="number"
                @click="onAnswer(number)"
            >{{ number }}</button>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            x: mtRand(100, 200),
            y: mtRand(100, 200)
        }
    },
    computed: {
        right() {
            return this.x + this.y;
        },
        answers(){
            let res = [this.right];

            while(res.length < 4) {
                let num = mtRand(this.right - 20, this.right + 20);
                if (res.indexOf(num) === -1) {
                    res.push(num);
                }
            }

            for (let i = res.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [res[i], res[j]] = [res[j], res[i]];
            }

            return res;
        }
    },
    methods: {
        onAnswer(num){
            if(num == this.right){
                this.$emit('success');
            } else {
                this.$emit('fail', `${this.x} + ${this.y} = ${this.right}!`);
            }
        }
    }
}

function mtRand(min, max) {
    let diff = max - min;
    return Math.floor(Math.random() * (diff + 1)) + min;
}

</script>

<style lang="scss" scoped>
    .btn {
        margin: 25px;
    }
</style>

