<script>
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';
import AppHeader from '../components/AppHeader.vue';
import AppFooter from '../components/AppFooter.vue';
export default {
    data() {
        return {
            projects:[],
            currentPage:1,
            lastPage:1
        };
    },
    methods: {
        nextPage(){
            if(this.currentPage < this.lastPage){
                axios
            .get('http://localhost:8000/api/projects',{
                params:{
                    page: this.currentPage + 1
                }
            })
            .then(response => {
            this.projects = response.data.result.data;
            this.currentPage = response.data.result.current_page;
            this.lastPage = response.data.result.last_page;
            })
            .catch(error => {
            console.error('Errore nella chiamata API:', error);
            });
            }
        },
        prevPage(){
            if(this.currentPage > 1 ){
                axios
            .get('http://localhost:8000/api/projects',{
                params:{
                    page: this.currentPage - 1
                }
            })
            .then(response => {
            this.projects = response.data.result.data;
            this.currentPage = response.data.result.current_page;
            this.lastPage = response.data.result.last_page;
            })
            .catch(error => {
            console.error('Errore nella chiamata API:', error);
            });
            }
        },
        getPage(i){
               axios
            .get('http://localhost:8000/api/projects',{
                params:{
                    page: i + 1
                }
            })
            .then(response => {
            this.projects = response.data.result.data;
            this.currentPage = response.data.result.current_page;
            this.lastPage = response.data.result.last_page;
            console.log(i)
            })
            .catch(error => {
            console.error('Errore nella chiamata API:', error);
            });
        }
    },
    components:{
        ProjectCard,
        AppFooter
    },
    created() {
        axios
            .get('http://localhost:8000/api/projects',{
                params:{
                    page: this.currentPage
                }
            })
            .then(response => {
            console.log(response.data);
            this.projects = response.data.result.data;
            this.currentPage = response.data.result.current_page;
            
            this.lastPage = response.data.result.last_page;
            })
            .catch(error => {
            console.error('Errore nella chiamata API:', error);
            });
        }
}
</script>

<template>
    <main>
        <h5 class="text-center mb-5">Pagina corrente: {{ currentPage }}</h5>
        <div class="container-fluid d-flex justify-content-center ">
                <ProjectCard
                v-for="(project,j) in projects"
                :project="project"
                :key="j"
                />
        </div>
        <div class="button-box d-flex justify-content-center mt-5">
            <nav aria-label="Page navigation example">
                <ul class="pagination ">
                    <li @click="prevPage()" class="page-item"><a class="page-link text-dark" href="#">Previous</a></li>
                    <li @click="getPage(i)" v-for="(page, i) in lastPage" :key="i" class="page-item "><a class="page-link text-dark" href="#">{{ page }}</a></li>
                    <li  @click="nextPage()" class="page-item"><a class="page-link text-dark" href="#">Next</a></li>
                </ul>
            </nav>
        </div>
    </main>
    <AppFooter />
</template>

<style lang="scss" scoped>
@use "../assets/scss/main.scss" as *;
main{
    height: calc(100vh - 200px);
    h5{
        margin:0 auto;
    }
    width: 100%;
    .button-box{
        width: 50%;
        margin: 0 auto;
    }
}
</style>
