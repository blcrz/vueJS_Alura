<template>
    <button @click="disparaAcao()" :class="estiloDoBotao" :type="tipo">{{ rotulo }}</button>
</template>

<script>
export default {

    props: {
            tipo: {
                required: true,
                type: String
            },

            rotulo: {
                required: true,
                type: String
            },

            confirmacao: {
                required: false,
                default: false,
                type: Boolean
            },

            estilo: {
                required: false,
                default: 'padrao',
                type: String
            }
        },

    computed: {

       estiloDoBotao() {

           // se o valor é padrão ou não passou nada para estilo
           if(this.estilo == 'padrao') return 'botao botao-padrao';

           if(this.estilo == 'perigo') return 'botao botao-perigo';
       }
    },

    methods: {

        disparaAcao() {
            if (this.confirmacao) {
                if(confirm('Confirma deleção?')) {
                    this.$emit('botaoAtivado', new Date())
                }
                return
            }
            this.$emit('botaoAtivado')
        }
    }
}
</script>

<style scoped>
    .botao {
        display: inline-block;
        padding: 10px;
        border-radius: 3px;
        margin: 10px;
        font-size: 1.2em;
    }

    .botao-perigo {
        background: firebrick;
        color: white;
    }

    .botao-padrao {
        background: darkcyan;
        color: white;
    }

</style>