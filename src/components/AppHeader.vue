<script>
export default {
    name: 'AppHeader',
}
</script>

<template>
    <router-link :to="{ name : 'home'}" class="text-decoration-none">
        <div class="d-flex justify-content-center align-items-center">
            <img class="img-fluid mx-auto" src="../assets/Boolfolio.png" alt="Lookas Logo">
        </div>
    </router-link>
</template>

<style lang="scss" scoped></style>