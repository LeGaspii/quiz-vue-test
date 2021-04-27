<template>
    <div class="question-boc-container">
        <b-jumbotron>
            <template #lead>
                {{ currentQuestion.question}}
            </template>

            <hr class="my-4">

            <ul class="list-group mb-2">
                <li class="list-group-item" 
                    v-for="(answer, index) in answers" 
                    :key="index"
                    @click.prevent="selectAnswer(index)"
                    :class="[selectIndex === index ? 'selected' : '']"
                >
                    {{answer}}
                </li>
            </ul>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button @click="next" variant="success" href="#">Next Question</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props: {
        currentQuestion: Object,
        next: Function
    },
    data() {
        return {
            selectIndex: null
        }
    },
    computed: {
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    },
    methods: {
        selectAnswer(index) {
            this.selectIndex = index
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
    background-color: lightsalmon;
}
</style>