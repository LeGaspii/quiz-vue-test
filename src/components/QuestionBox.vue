<template>
    <div class="question-boc-container">
        <b-jumbotron>
            <template #lead>
                {{ currentQuestion.question}}
            </template>

            <hr class="my-4">

            <p>
            Réponses
            </p>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button variant="success" href="#">Next Question</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props: {
        currentQuestion: Object
    }
}
</script>