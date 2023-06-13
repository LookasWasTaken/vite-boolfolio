<script>
import axios from 'axios';
export default {
    name: "App",
    components:{

    },
    data(){
        return{
            host: 'http://127.0.0.1:8000/',
            projectsEndPoint: 'api/projects',
            imgEndPoint: 'storage/',
            projects: null,
            
        }
    },
    methods: {

    },
    mounted(){
        const URL = this.host + this.projectsEndPoint;
        axios.get(URL)
        .then(response => {
            this.projects = response.data.projects.data;
        })
        .catch(error =>{
            console.error(error)
        })
    },
}
</script>

<template>
<div class="container">
    <h1 class="text-center py-5 text-light">LookasWasTaken BoolFolio</h1>
    <div class="row row-cols-3 g-5">
        <div class="col" v-for="(project, index) in projects">
            <div class="card h-100">
                <div class="card-header bg-danger text-light">
                    <h5 class="my-3 text-center text-uppercase fw-bold">{{ project.name }}</h5>
                </div>
                <div class="card-body px-0 d-flex justify-content-around align-items-center">
                        <img width=150 class="img-fluid rounded shadow" :src="host + imgEndPoint + project.image" :alt="project.name + ' img'">
                        <div class="data_info text-center">
                            <p class="badge" :class="project.type.color" v-if="project.type">{{ project.type.name }}</p>
                            <hr>
                            <p class="fw-bold fs-6">updated x ago</p>
                            <hr>
                            <template v-if="project.technologies">
                                <p class="badge m-1" :class="technology.color" v-for="(technology, index) in project.technologies">{{ technology.name }}</p>
                            </template>
                            
                        </div>
                </div>
                <div class="card-footer py-2 text-center">
                    <a class="text-decoration-none fs-6" :href="project.repo">LookasWasTaken/{{ project.slug }}</a>
                </div>
            </div>
        </div>

    </div>
</div>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>
