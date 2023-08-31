<template >
    <div>
        <h1 class="main-title">
            Projects:
        </h1>
        <div class="projects">
            <div :style="'border: 2px solid' + project.type.color + ';'" class="single-project" v-for="project in projects">
                <h2>
                    {{ project.title }}
                </h2>
                <h4 :style="'color:' + project.type.color + ';'">
                    Type: {{ project.type.name }}
                </h4>
                
                <p>
                    {{ project.content.substr(0, 250) }}
                </p>
                <h5>
                    <span v-for="technology in project.technologies">#{{ technology.name }} </span>
                </h5>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'AppMain',

    data() {
        return {
            projects : [],
            apiUrl : 'http://127.0.0.1:8000/api/projects'
        }
    },

    methods: {
        getprojects(){
            // recuper i miei project e popolo la variabile projects
            axios.get(this.apiUrl, {
                params: {}
            })
            .then((response) => {
                console.log(response.data.results.data)
                this.projects = response.data.results.data;
            })
            .catch(function (error) {
                console.log(error);
            })
        }
    },

    created(){
        this.getprojects();
    }
}

</script>

<style lang="scss">

    h1.main-title{
        margin-bottom: 3rem;
    }

    div.projects{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        gap: 1rem;

        div.single-project{
            width: calc((100% / 2) - 3.5rem);
            height: 20rem;
            border-radius: 1rem;
            padding: 1rem;
            background-color: #fff;
            color: black;
            margin-bottom: 2rem;
            font-family: cursive;

            *{
                margin-bottom: .75rem;
            }

            h5 span{
                margin-right: 1rem;
            }

            &:hover{
                background-color: #eee;
            }
        }
    }
</style>