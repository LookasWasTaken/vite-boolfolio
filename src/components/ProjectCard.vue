<script>
export default {
    name: 'ProjectCard',
    props: {
        project: Object,
        host: String,
        imgEndPoint: String,
    }
}
</script>

<template>
    <div class="card h-100">
        <div class="card-header bg-danger">
            <router-link class="text-decoration-none text-light" :to="{ name : 'single-project', params: { slug: project.slug } }">
                <h5 class="my-3 text-center text-uppercase fw-bold">{{ project.name }}</h5>
            </router-link>
        </div>
        <div class="card-body px-0 d-flex justify-content-evenly align-items-center">
            <img width=150 class="img-fluid rounded shadow" :src="host + imgEndPoint + project.image"
                :alt="project.name + ' img'">
            <div class="data_info text-center w-50">
                <p class="badge" :class="project.type.color" v-if="project.type">{{ project.type.name }}</p>
                <hr>
                <p class="fw-bold fs-6">Update {{ project.date }}</p>
                <hr>
                <template v-if="project.technologies">
                    <p class="badge m-1" :class="technology.color" v-for="(technology, index) in project.technologies">{{
                        technology.name }}</p>
                </template>

            </div>
        </div>
        <div class="card-footer py-2 text-center">
            <a class="text-decoration-none fs-6" :href="project.repo">LookasWasTaken/{{ project.slug }}</a>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>