<template>
    <div class="loader">
        <span class="loader-1"></span>
        <span class="loader-2"></span>
        <span class="loader-3"></span>
    </div>
</template>

<style scoped>
.loader {
    padding: 10px 0 0 0;
    display: flex;
    gap: 5px;
}
.loader span {
    background-color: rgb(0, 0, 0);
    border-radius: 50%;
    width: 6px;
    height: 6px;
    opacity: 0.1;
}
.loader-1 {
    animation: loading 0.8s 0s infinite linear;
}
.loader-2 {
    animation: loading 0.8s 0.1s infinite linear;
}
.loader-3 {
    animation: loading 0.8s 0.2s infinite linear;
}
@keyframes loading {
    80%{
        opacity: 0.1;
    }
    100%{
        opacity: 1;
    }
}
</style>