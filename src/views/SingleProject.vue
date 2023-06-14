<script>
import axios from 'axios';
export default {
    name: "SingleProject",
    components: {

    },
    data() {
        return {
            host: 'http://127.0.0.1:8000/',
            projectsEndPoint: 'api/projects',
            imgEndPoint: 'storage/',
            project: null,

        }
    },
    methods: {

    },
    mounted() {
        const URL = this.host + this.projectsEndPoint + "/" + this.$route.params.slug;
        axios.get(URL)
            .then(response => {
                if (response.data.success) {
                    this.project = response.data.project;
                } else {
                    this.$router.push({ name: 'not-found' })
                }
            })
            .catch(error => {
                console.error(error)
            })
    },
}
</script>

<template>
    <div class="container" v-if="this.project">
        <div class="row">
            <div class="col-6 mx-auto">
                <div class="card">
                    <div class="card-header bg-danger">
                        <h1 class="text-center text-light py-3 text-uppercase">{{ project.name }}</h1>
                    </div>
                    <div class="card-body px-0 py-5 d-flex justify-content-evenly align-items-center">
                        <img width=200 class="img-fluid rounded shadow" :src="host + imgEndPoint + project.image"
                            :alt="project.name + ' img'">
                        <div class="data_info text-center w-50">
                            <p class="badge" :class="project.type.color" v-if="project.type">{{ project.type.name }}</p>
                            <hr>
                            <p class="fw-bold fs-6">updated x ago</p>
                            <hr>
                            <template v-if="project.technologies">
                                <p class="badge m-1" :class="technology.color"
                                    v-for="(technology, index) in project.technologies">{{
                                        technology.name }}</p>
                            </template>
                        </div>
                    </div>
                    <div class="card-footer py-5 text-center">
                        <a class="text-decoration-none fs-4" :href="project.repo">LookasWasTaken/{{ project.slug }}</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>