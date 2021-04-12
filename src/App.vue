<template>
    <div id="app">
        <div class="top">
            <img alt="Vue logo" src="./assets/logo.svg" height="200" />
        </div>
        <div class="content">
            <Question :qText="gameQuest.text" />
            <div class="answers">
                <div
                    v-for="ans in gameQuest.answers"
                    :key="ans"
                    ref="risposta"
                    @click="check($event, ans)"
                >
                    <Answer :aText="ans" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Question from "./components/Question";
import Answer from "./components/Answer";

export default {
    name: "App",
    components: {
        Question,
        Answer,
    },
    data() {
        return {
            questions: [
                {
                    id: 1,
                    text:
                        "Di quale regione italiana è originario Carmelo Bene?",
                    answers: {
                        a: "Puglia",
                        b: "Basilicata",
                        c: "Sicilia",
                        d: "Toscana",
                    },
                    correctAns: "Puglia",
                },
                {
                    id: 2,
                    text:
                        "Come si intitola il primo album da solista di Francesco Bianconi?",
                    answers: {
                        a: "Il bene",
                        b: "Forever",
                        c: "L'abisso",
                        d: "Boudelaire",
                    },
                    correctAns: "Forever",
                },
                {
                    id: 3,
                    text:
                        "Quale animale è presente nel logo della marca di sigarette Winston?",
                    answers: {
                        a: "Puma",
                        b: "Aquila",
                        c: "Giaguaro",
                        d: "Canguro",
                    },
                    correctAns: "Aquila",
                },
                {
                    id: 4,
                    text:
                        "In quale regione italiana si trova il monte Zoncolan?",
                    answers: {
                        a: "Veneto",
                        b: "Trentino",
                        c: "Piemonte",
                        d: "Friuli",
                    },
                    correctAns: "Friuli",
                },
                {
                    id: 5,
                    text:
                        "In quale anno è stato pubblicato 'Animals', capolavoro dei Pink Floyd?",
                    answers: {
                        a: 1979,
                        b: 1975,
                        c: 1970,
                        d: 1973,
                    },
                    correctAns: 1973,
                },
                {
                    id: 6,
                    text:
                        "Quale di questi film non è stato musicato da Ennio Morricone?",
                    answers: {
                        a: "Il buono, il brutto e il cattivo",
                        b:
                            "Indagine su un cittadino al di sopra di ogni sospetto",
                        c: "Mission",
                        d: "Novecento",
                    },
                    correctAns: "Novecento",
                },
            ],
            gameQuest: {},
            points: 0,
        };
    },
    methods: {
        check(event, answer) {
            const allAns = this.$refs.risposta;
            const clickedAns = allAns.filter(
                (risposta) => risposta.innerText == answer
            )[0];

            if (clickedAns.innerText == this.gameQuest.correctAns) {
                event.target.style.background = "green";
                this.points++;
            } else {
                event.target.style.background = "red";
            }

            // tolgo la domanda dall'array e aggiorno l'array
            const updatedQuestions = this.questions.filter(
                (question) => question != this.gameQuest
            );
            this.questions = updatedQuestions;
            console.log(this.questions);

            // attesa di 2s e cambia la domanda - nel caso di esaurimento delle domande esce un alert
            setTimeout(() => {
                if (this.questions.length == 0) {
                    alert(
                        `Gioco finito. Hai risposto correttamente a ${this.points} domande su 6.`
                    );
                    window.location.href = "/";
                } else {
                    if (this.questions.length > 1) {
                        this.randomQuest();
                    } else {
                        this.gameQuest = this.questions[0];
                    }
                }
            }, 1000);
        },
        randomQuest() {
            const randIdx = Math.floor(Math.random() * this.questions.length);
            this.gameQuest = this.questions[randIdx];
        },
    },
    mounted() {
        this.randomQuest();
    },
};
</script>

<style lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    background: #12093a;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    // text-align: center;
    // color: #2c3e50;
    // margin-top: 60px;
}

.top {
    width: 100%;
    padding: 1.5rem;
    background: rgb(58, 61, 180);
    background: linear-gradient(
        90deg,
        rgba(58, 61, 180, 1) 0%,
        rgba(29, 31, 253, 1) 50%,
        rgba(58, 61, 180, 1) 100%
    );
    display: grid;
    place-items: center;
}

.content {
    padding: 2rem;

    .answers {
        margin-top: 4rem;
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 3rem;
    }
}

@media (max-width: 700px) {
    .content .answers {
        grid-template-columns: 1fr;
        gap: 2rem;
    }
}
</style>
