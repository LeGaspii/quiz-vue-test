<template>
    <div class="question-boc-container">
        <b-jumbotron>
            <template #lead>
                {{ currentQuestion.question}}
            </template>

            <hr class="my-4">

            <ul class="list-group mb-2">
                <li class="list-group-item" 
                    v-for="(answer, index) in shuffledAnswers" 
                    :key="index"
                    @click.prevent="selectAnswer(index)"
                    :class="answerClass(index)"
                >
                    {{answer}}
                </li>
            </ul>

            <b-button 
                variant="primary"
                @click="submitAnswer"
                :disabled="selectIndex = null || answered"
                >Submit
            </b-button>
            <b-button @click="next" variant="success" href="#">Next Question</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from 'lodash'
export default {
    props: {
        currentQuestion: Object,
        next: Function,
        increment: Function
    },
    data() {
        return {
            selectIndex: null,
            shuffledAnswers: [],
            correctIndex: null,
            answered: false
        }
    },
    computed: {
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    },
    watch: {
        currentQuestion: {
            immediate: true,
            handler() {
                this.selectIndex = null
                this.shuffleAnswers()
                this.answered = false
            }
        }
    },
    methods: {
        selectAnswer(index) {
            this.selectIndex = index
        },
        submitAnswer() {
            let isCorrect = false
            if (this.selectIndex === this.correctIndex) {
                isCorrect = true
            }
            this.answered = true
            this.increment(isCorrect)
        },
        shuffleAnswers() {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers)
            this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
        },
        answerClass(index) {
            let answerClass = ''
            if (!this.answered && this.selectIndex === index) {
                answerClass = 'selected'
            } else if (this.answered && this.correctIndex === index) {
                answerClass = 'correct'
            } else if (this.answered && 
            this.selectIndex === index && 
            this.correctIndex !== index) {
                answerClass = 'incorrect'
            }
            return answerClass
        }
    }
}
</script>


<style scoped>
.list-group {
    margin-bottom: 15px;
}
.list-group-item:hover {
    background: #eee;
    cursor: pointer;
}
.btn {
    margin: 0 5px;
}
.selected {
    background-color: lightblue;
}

.correct {
    background-color: lightgreen;
}

.incorrect {
    background-color: red;
}
</style>