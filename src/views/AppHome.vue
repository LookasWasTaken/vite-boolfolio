<script>
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';
export default {
    name: "AppHome",
    components: {
        ProjectCard
    },
    data() {
        return {
            host: 'http://127.0.0.1:8000/',
            projectsEndPoint: 'api/projects',
            imgEndPoint: 'storage/',
            projects: null,
            nextURL: null,
            prevURL: null,
            currentPage: 1,
            loading: true,

        }
    },
    methods: {
        prevPage(URL) {
            this.getProjects(URL);
        },
        nextPage(URL) {
            this.getProjects(URL);
        },
        getProjects(URL) {
            axios.get(URL)
                .then(response => {
                    this.projects = response.data.projects.data;
                    this.nextURL = response.data.projects.next_page_url;
                    this.prevURL = response.data.projects.prev_page_url;
                    this.currentPage = response.data.projects.current_page;
                    this.loading = false;
                })
                .catch(error => {
                    console.error(error)
                })
        }
    },
    mounted() {
        const URL = this.host + this.projectsEndPoint;
        this.getProjects(URL)
    },
}
</script>

<template>
    <div v-if="loading">
        <div class="row row-cols-3 g-5">
            <div class="col" v-for="n in 3">
                <div class="card" aria-hidden="true">
                <img src="..." class="card-img-top" alt="...">
                <div class="card-body">
                    <h5 class="card-title placeholder-glow">
                        <span class="placeholder col-6"></span>
                    </h5>
                    <p class="card-text placeholder-glow">
                        <span class="placeholder col-7"></span>
                        <span class="placeholder col-4"></span>
                        <span class="placeholder col-4"></span>
                        <span class="placeholder col-6"></span>
                        <span class="placeholder col-8"></span>
                    </p>
                    <a href="#" tabindex="-1" class="btn btn-primary disabled placeholder col-6"></a>
                </div>
            </div>
            </div>
        </div>
    </div>
    <div v-else class="row row-cols-3 g-5">
        <div class="col" v-for="(project, index) in projects">
            <ProjectCard :project="project" :host="host" :imgEndPoint="imgEndPoint"></ProjectCard>
        </div>
    </div>
    <nav aria-label="Page navigation" class="py-4 text-center" v-if="projects">
        <ul class="pagination align-items-center justify-content-center">
            <li class="page-item">
                <button class="page-link" aria-label="Previous" @click="prevURL ? prevPage(prevURL) : ''">
                    <span aria-hidden="true">&laquo;</span>
                </button>
            </li>
            <li>
                <button class="page-link" aria-label="current_page">
                    <span aria-hidden="true">{{ this.currentPage }}</span>
                </button>
            </li>
            <li class="page-item">
                <button class="page-link" aria-label="Next" @click="nextURL ? nextPage(nextURL) : ''">
                    <span aria-hidden="true">&raquo;</span>
                </button>

            </li>
        </ul>
    </nav>
</template>

<style lang="scss" scoped></style>