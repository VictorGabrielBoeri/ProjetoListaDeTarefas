<template>
    <section>
        <form @submit.prevent="salvar">
            <div class="field mb-4">
                <label class="label title-modo-escuro mb-3" for="nomeDoProjeto">
                    Nome Do Projeto
                </label>
                <input class="input mb-3" type="text" v-model="nomeDoProjeto" id="nomeDoProjeto">
                <div class="field">
                    <button class="button" type="submit">Salvar</button>
                </div>
            </div>
        </form>
    </section>
</template>

<script lang="ts">
import { useStore } from '@/store';
import { ALTERA_PROJETO, ADICIONA_PROJETO } from '@/store/tipo-mutacoes';
import { defineComponent } from 'vue';
import { TipoNotificacao } from '@/interfaces/INotificacao';
import useNotificador from '@/hooks/notificador';


export default defineComponent({
    name: 'PaginaFormulario',
    props: {
        id: {
            type: String
        }
    },
    mounted() {
        if (this.id) {
            const projeto = this.store.state.projetos.find(proj => proj.id == this.id)
            this.nomeDoProjeto = projeto?.nome || ''
        }
    },
    data() {
        return {
            nomeDoProjeto: ""
        }
    },
    methods: {
        salvar() {
            if (this.id) {
                this.store.commit(ALTERA_PROJETO, {
                    id: this.id,
                    nome: this.nomeDoProjeto,
                })
                this.notificar(TipoNotificacao.ATENCAO, 'Editado!', 'O projeto foi editado')
            } else {
                this.store.commit(ADICIONA_PROJETO, this.nomeDoProjeto)
            }
            this.nomeDoProjeto = '';
            this.notificar(TipoNotificacao.SUCESSO, 'Exelente!', 'O projeto foi criado com sucesso')
            this.$router.push('/projetos')
        },
    },
    setup() {
        const store = useStore()
        const { notificar } = useNotificador()
        return {
            store,
            notificar
        }
    }
})
</script>