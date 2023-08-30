<template>
    <div class="message">
        <slot></slot>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
.message {
    padding: 10px;
    background-color: #FFFFFF;
    color: black;
    border-radius: 12px;
    width: fit-content;
    max-width: 60%;
}
</style>