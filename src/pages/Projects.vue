<template lang="">
    <section class="projects-wrapper">
        <h1 class="main-title">
            Latest projects:
        </h1>
        <nav class="pagination">
            <li class="prev" @click="prevPage" v-if="prevPageUrl">
                Previous
            </li>
            <li class="next" @click="nextPage" v-if="nextPageUrl">
                Next
            </li>
        </nav>
        <div class="projects">
            <SingleProject class="single-project w-50" v-for="project in projects" :project='project'
                @click="$router.push({ name: 'projects.show', params: { slug: project.slug} })" />
        </div>
    </section>
</template>

<script>
import axios from 'axios';
import SingleProject from '../components/SingleProject.vue';

export default {
    name: 'Projects',
    components: {
        SingleProject
    },
    data() {
        return {
            projects : [],
            nextPageUrl : '',
            currentPageNo: '',
            prevPageUrl : '',
            apiUrl : 'http://127.0.0.1:8000/api/projects'
        }
    },

    methods: {
        getProjects(apiUrl = this.apiUrl){
            // recuper i miei project e popolo la variabile projects
            axios.get(apiUrl)
            .then((response) => {
                console.log(response)
                this.projects = response.data.results.data;
                this.nextPageUrl = response.data.results.next_page_url;
                this.prevPageUrl = response.data.results.prev_page_url;
            })
            .catch(function (error) {
                console.log(error);
            })
        },

        nextPage(){
            // alert('next page');
            this.getProjects(this.nextPageUrl);
        },

        prevPage(){
            // alert('prev page');
            this.getProjects(this.prevPageUrl);
        },

    },

    created(){
        this.getProjects();
    }
}

</script>
<style lang="scss" scoped>
    h1.main-title{
        margin-bottom: 3rem;
    }
    div.projects{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
    }

    nav.pagination{
        width: 100%;
        padding: 1rem;
        display: flex;
        // justify-content: space-between;
        align-items: center;
        background-color: black;
        list-style-type: none;

        li{
            padding: 1rem;
            background-color: blue;
            color: white;

            &.next{
                margin-left: auto;
            }
        }
    }
</style>