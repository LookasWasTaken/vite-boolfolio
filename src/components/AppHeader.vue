<script>
export default {
    name: 'AppHeader',
}
</script>

<template>
    <router-link :to="{ name : 'home'}" class="text-decoration-none">
        <h1 class="text-center py-5 text-light">LookasWasTaken BoolFolio</h1>
    </router-link>
</template>

<style lang="scss" scoped></style>