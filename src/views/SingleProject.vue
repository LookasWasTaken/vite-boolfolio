<script>
import axios from 'axios';
export default {
    name: "SingleProject",
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
    
</template>

<style lang="scss" scoped>
</style>