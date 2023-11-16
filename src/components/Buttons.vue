<template>
    <button @click="$emit('btnAddValue', btnValue)" class="btn">{{ btnValue }}</button>
</template>

<script>
export default {
    name: 'buttons',
    props: {
        btnValue: String
    }
}
</script>

<style scoped>
.btn {
    border-radius: 4px;
    font-size: 35px;
    flex: 1;
    height: 2.2em;
    margin: 1px;
    border: none;
    background-color: #18597a;
    color: #e5e5b9;
}

.btn:hover {
    background-color: #1b658a;
    transition: .2s;
}

.btn:active {
    background-color: #134761;
    transition: .1s;
}
</style>