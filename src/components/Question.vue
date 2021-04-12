<template>
    <div class="question">
        <h3>{{ qText }}</h3>
    </div>
</template>

<script>
export default {
    name: "Question",
    props: {
        qText: String,
    },
};
</script>

<style lang="scss" scoped>
h3 {
    font-size: 1.5rem;
    color: #fff;
    display: grid;
    place-items: center;
    width: 70vw;
    height: 80px;
    margin: 0 2rem;
}

.correct {
    background: green;
}
</style>
