<script>
import Questions from './components/Questions.vue'
import Result from './components/Result.vue'

export default {
    name: "App",
    components: {
        Questions,
        Result
    },
    data() {
        return {
            questionsAnswered: 0,
            totalCorrect: 0,
            questions: [
                {
                    q: 'What is (8 - 2) * 2?', 
                    answers: [
                        {
                            text: '4',
                            is_correct: false
                        },
                        {
                            text: '12',
                            is_correct: true 
                        },
                        {
                            text: '6',
                            is_correct: false 
                        },
                        {
                            text: '8',
                            is_correct: false 
                        }
                    ] 
                },
                { 
                    q: 'What is the largest country in the world?', 
                    answers: [
                        {
                            text: 'China',
                            is_correct: false
                        },
                        {
                            text: 'Canada',
                            is_correct: false 
                        },
                        {
                            text: 'Russia',
                            is_correct: true 
                        },
                        {
                            text: 'Luxembourg',
                            is_correct: false 
                        }
                    ] 
                },
                { 
                    q: 'Where do kangaroos live?', 
                    answers: [
                        {
                            text: 'Austria',
                            is_correct: false
                        },
                        {
                            text: 'China',
                            is_correct: false 
                        },
                        {
                            text: 'Australia',
                            is_correct: true 
                        },
                        {
                            text: 'Brazilia',
                            is_correct: false 
                        }
                    ] 
                }
            ],
            results: [
                {
                    min: 0,
                    max: 2,
                    title: "No way. Try again!",
                    desc: "Do a little more studying and you may succeed!"
                },
                {
                    min: 3,
                    max: 3,
                    title: "You're a genius!",
                    desc: "Studying has definitely paid off for you!"
                }
            ]
        }
    },
    methods: {
        questionAnswered(is_correct) {
            if (is_correct) { this.totalCorrect++; }
            this.questionsAnswered++;
        },
        resetQuiz() {
            this.questionsAnswered = 0;
            this.totalCorrect = 0;
        }
    }
}
</script>

<template>
    <div class="ctr">
        <transition name="fade" mode="out-in">
            <questions v-if="questionsAnswered < questions.length" :questions="questions" :questionsAnswered="questionsAnswered" @question-answered="questionAnswered"/>
            <result v-else :results="results" :totalCorrect="totalCorrect" />
        </transition>

        <button type="button" class="reset-btn" @click.prevent="resetQuiz" v-if="this.questionsAnswered === questions.length">Reset</button>
    </div>
</template>