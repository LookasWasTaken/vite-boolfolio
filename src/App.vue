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
    <div class="row row-cols-2">
        <div class="col" v-for="(project, index) in projects">
            <div class="card">
                {{ project.name }}
            </div>
        </div>

    </div>
</div>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>
