<script>
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';
export default {
    name: "AppHome",
    components:{
    ProjectCard
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
    <div class="row row-cols-3 g-5">
        <div class="col" v-for="(project, index) in projects">
            <ProjectCard :project="project" :host="host" :imgEndPoint="imgEndPoint"></ProjectCard>
        </div>

    </div>
</template>

<style lang="scss" scoped>
</style>