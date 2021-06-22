<template>
    <section class="second">
        <div class=" container"><!--container-->
            <div class="filter"><!--bloco de filtragem por select-->
                <legend>Nome</legend>
                <input type="text" v-model="filter">
            </div>
            <div class="filter">  
                <legend>Gênero</legend>
                <input v-model="gender" type="radio" name="gender" value="male">
                <label>Masculino</label>
                <input v-model="gender" type="radio" name="gender" value="female">
                <label>Feminino</label>
            </div> 
            <div class="filter"> 
                <legend>Status</legend>
                <input type="radio" v-model="status" name="status" value="alive">
                <label>Vivo</label>
                <input type="radio" v-model="status" name="status" value="dead">
                <label>Morto</label>
            </div>
            <div class="filter">
                <input @click="mountedUrl" type="button" value="Pesquisar">
                <input @click="resetUrl" type="button" value="Resetar">
            </div><!--fim do blodo de filtros-->
            <div class="picture"><!--área de exibição dos personagens-->
                <div v-if="list.length">
                <div class="character" v-for="(item, i) in list" :key="i" >
                    <img :src="item.image"/>
                    <h3>Name: {{ item.name }}</h3>
                    <h4>Status: {{ item.status }}</h4>
                    <h4>Species: {{ item.species }}</h4>
                    <h4>Gender: {{ item.gender }}</h4>
                </div>
                </div>
                <p v-else >Resultado não encontrado</p>
            </div>
            <button @click="changePage"> >> </button><!--Botao de troca de página-->
        </div><!--fim do container-->
    </section>
    
</template>

<script>
import axios from 'axios'

export default {
    name: 'Section-third',
    data: () => ({
        list: [],
        filter: '',
        gender: '',
        status: '',
        url: 'https://rickandmortyapi.com/api/character/?page=1'
    }),
    methods: {
//montagem da url
        mountedUrl(){
            let str = '';
            this.url = 'https://rickandmortyapi.com/api/character/?page=1';
            if(this.filter) str = `&name=${this.filter}`;
            if(this.status) str = `${str}&status=${this.status}`;
            if(this.gender) str = `${str}&gender=${this.gender}`;
            this.url = `${this.url}${str}`;
            this.request();
        },
//reset da url
        resetUrl(){
            this.url = 'https://rickandmortyapi.com/api/character/?page=1';
            this.filter = '';
            this.gender = '';
            this.status = '';
            this.request();
        },
//mudar pagina
        changePage(){
            if (this.url == 'https://rickandmortyapi.com/api/character/?page=1')
            this.url = 'https://rickandmortyapi.com/api/character/?page=2';
            else this.url = 'https://rickandmortyapi.com/api/character/?page=1'
            this.request();
        },
//requisicao
        request() {
            axios.get(this.url)
            .then((response)=> {
                this.list = response.data.results;
            })
            .catch(()=> {
               this.list = [];
            })
        },
    },
    mounted(){
        this.request();
    },
}
</script>

<style scoped>

/* Estilo filtros*/
section.second{
    background-color: #24282f;
}


section div.filter{
    width: 25%;
    float: left;
    margin-top: 20px;
}

div.filter [type=text]{
    height: 24px;
    width: 150px;
    font-size: 15px;
    font-weight: 600;
}


div.filter legend{
    color: white;
    font-size: 20px;
    padding: 5px 10px;
}

div.filter label{
    color: white;
    padding: 0px 5px;
}

div.filter input[type=button]{
    width: 110px;
    height: 24px;
    margin: 35px 2px;
    font-size: 16px;
    color: #24282f;
    background-color: white;
    border-radius: 5px;
    font-weight: 600;
}


/*estilo personagens*/
div.picture{
    width: 100%;
    background-color: #24282f;
    display: flex;
    flex-wrap: wrap;
    min-height: 500px;
}

div.picture div:not(.character){
    width: 100%;
    display: flex;
    flex-wrap: wrap;
}

div.picture p{
    color: white;
    padding: 20px 20px;
}

div.character{
    width: calc( 100% / 3);
    background-color: rgb(173, 173, 173);
    border: 5px solid #24282f;
    border-radius: 10px;
    margin: 20px 0;

}

div.character img{
    width: 230px;
    height: 220px;
    border-radius: 10px;
    padding-top: 5px;
}

div.character h3{
    color: #24282f;
    font-size: 20px;
}

div.character h4{
    color: #24282f;
    font-size: 20px;
    margin-top: 5px;
}

div.container > button{
    position: relative;
    background-color: white;
    width: 75px;
    height: 24px;
    color: #24282f;
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 30px;
    border-radius: 5px;
}
</style>