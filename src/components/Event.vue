<template>
    <span :class="{ type }"
        ><p>{{ date }}&nbsp;{{ name }}</p></span
    >
</template>

<script>
export default {
    props: {
        id: Number,
        name: String,
        date: Number,
        type: String,
    },
}
</script>

<style lang="scss">
.red p {
    background-color: #fceced;
    color: #c78587;
    border-radius: 5px;
    padding: 0 3px 0 3px;
    margin: 3px;
    text-align: left;
    cursor: pointer;
}

.yellow p {
    background-color: #f7ecd8;
    color: #cfaf7d;
    border-radius: 5px;
    padding: 0 3px 0 3px;
    margin: 3px;
    text-align: left;
    cursor: pointer;
}

.green p {
    background-color: #eaf5ed;
    color: #a6d3b2;
    border-radius: 5px;
    padding: 0 3px 0 3px;
    margin: 3px;
    text-align: left;
    cursor: pointer;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    &:hover {
        position: absolute;
    }
}

div {
    display: inline-block;
    padding: 2px 5px 2px 5px;
    border-radius: 5px;
}
</style>
