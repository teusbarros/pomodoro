<template>
    <button class="btn-geral" :class="cor" @click="acao">{{nome}}</button>
</template>

<script>
export default {
    props: {
        nome: String,
        cor: Boolean,
        acao: Function
    }
}
</script>

<style>

.btn-geral {
    width: 130px;
    margin: 0 30px 0 30px;
    border-style: solid;
    border-width: 0 1px 1px 0;
    border-radius: 15px;
    background-color: #e2e2e2;
}
 *:focus {
    outline: 0 !important;
}

</style>