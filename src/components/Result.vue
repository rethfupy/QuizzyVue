<script>
export default {
    props: ['results', 'totalCorrect'],
    computed: {
        resultIndex() {
            let index = 0;
            this.results.forEach((result, i) => {
                if (result.min <= this.totalCorrect && result.max >= this.totalCorrect) {
                    index = i;
                }
            })
            return index;
        }
    }
}
</script>

<template>
    <div class="result">
        <div class="title">{{ results[resultIndex].title }}</div>
        <div class="desc">{{ results[resultIndex].desc }}</div>
    </div>
</template>