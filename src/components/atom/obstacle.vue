<template>
    <div class="quoridor__obstacle"></div>
</template>

<script>
export default {}
</script>

<style scoped>
.quoridor__obstacle {
    width: 100%;
    height: 5px;
    background-color: red; /* Cambiamos el color a rojo */
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}
</style>