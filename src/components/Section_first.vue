<template>
    <section class="first">
        <div class="container"><!--Container-->
            <h2>Personagens da Série</h2>
            <h2>Filtre os personagens pelas caraterísticas abaixo:</h2>
        </div><!--Container-->
    </section>
</template>

<script>


export default {
    name: 'Section_first',
   
}
</script>

<style>

section.first{
    width: 100%;
    background-color: #24282F;
}

section.firts > div.container{
    display: block;
}

.first h2{
    color: white;
    font-size: 28px;
    padding-top: 10px;
    margin: 0 auto;
}

</style>