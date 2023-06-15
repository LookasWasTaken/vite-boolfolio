<script>
import AppHeader from './components/AppHeader.vue';
export default {
    name: "App",
    components: {
        AppHeader,
    },
    data() {
        return {
        }
    }
}
</script>

<template>
    <div class="container pb-5">
        <AppHeader></AppHeader>
        <router-view></router-view>
    </div>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>
