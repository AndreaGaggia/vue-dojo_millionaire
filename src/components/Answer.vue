<template>
    <div class="answer">
        {{ aText }}
    </div>
</template>

<script>
export default {
    name: "Answer",
    props: ["aText"],
};
</script>

<style lang="scss" scoped>
.answer {
    padding: 1rem;
    color: #fff;
    display: grid;
    place-items: center;
    border: 1px solid white;
    border-end-end-radius: 0.5rem;
    border-start-start-radius: 0.5rem;
    cursor: pointer;
    font-size: 1.2rem;
    text-align: center;
}
</style>
