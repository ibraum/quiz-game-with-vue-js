<script setup>
    import Radio from './components/Radio.vue';
    import Next from './components/Next.vue';
    import QuestionLayout from './components/QuestionLayout.vue';
    import QuizLayout from './components/QuizLayout.vue';
    import Range from './components/Range.vue';

    import { quiz } from './Question.js';
    import { ref } from 'vue';

    const questions = ref([])
    const response = ref('')
    const minScore = ref()
    const failmsg = ref('')
    const succmsg = ref('')
    let currentQuestionNumber = ref(0)
    let name = ref('')
    let percent = ref(0)
    let currentPercent = ref(0)
    let score = ref(0)


    failmsg.value = quiz.failureMessage
    succmsg.value = quiz.successMessage
    minScore.value = quiz.minScore
    questions.value = quiz.questions
    percent.value = 100 / questions.value.length
    

    const getCurrentQuestion = () => {
        currentPercent.value = percent.value * (1 + currentQuestionNumber.value)
        name = questions.value[currentQuestionNumber.value].title
        return questions.value[currentQuestionNumber.value]
    }

    const getCurrentQuestionOptions = () => {
        return getCurrentQuestion().options
    }

    const isActive = ref(
        () => {
            if (response.value === 'T' || response.value === 'F') {
                return true
            }

            return false
        }
    )

    const isCorrectResponse = (event) => {
        if (response.value === 'T') {
            score.value++
            // response.value = ''
        } else{

        }

        nextQuestion()
    }

    const nextQuestion = () => {
        currentQuestionNumber.value++
        // click = ''
        console.log(currentQuestionNumber.value, score.value)
    }

    const currentQuestion = ref(getCurrentQuestion())
</script>   

<template>
    <div v-if="currentQuestionNumber < questions.length -1">
        <QuizLayout :title="'QUIZ SUR LES FILMS'" >
            <template v-slot:container>
                {{ score }}
                {{ minScore }}
                <Range :val="currentPercent">
                    {{ currentPercent }}
                </Range>
                <QuestionLayout :question="currentQuestion.question">
                    <template v-slot:questions>
                        <form action="" @submit.prevent="isCorrectResponse()">
                            <Radio v-for="option in getCurrentQuestionOptions()" :label="option.text" :nameValue="name" v-model="response" :value="option.isCorrect" :k="option.text"/>{{ response }}
                            <Next :content="'Question suivante'" :click="isActive"/>
                        </form>
                    </template>
                </QuestionLayout>
            </template>
        </QuizLayout>
    </div>
    <div v-else>
        <QuizLayout :title="'Vous êtes à la fin du quiz !'" > 
            <template v-slot:container>
                <div v-if="score < minScore">
                    <span>
                        {{ failmsg }}
                    </span>
                </div>
                <div v-else>
                    <span>
                        {{ succmsg }}
                    </span>
                </div>
            </template>
        </QuizLayout>
    </div>
</template>

<style scoped>

</style>