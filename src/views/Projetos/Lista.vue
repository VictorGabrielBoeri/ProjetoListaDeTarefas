<template>
    <section>
        <router-link to="/projetos/novo" class="button mb-5">
            <span class="icon is-small">
                <i class="fas fa-plus"></i>
            </span>
            <span>Novo projeto</span>
        </router-link>
        <table class="table is-fullwidth">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nome</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="projeto in projetos" :key="projeto.id">
                    <td>{{ projeto.id }}</td>
                    <td>{{ projeto.nome }}</td>
                    <td>
                        <router-link :to="`/projetos/${projeto.id}`" class="button">
                            <span class="icon is-small">
                                <i class="fas fa-pencil-alt"></i>
                            </span>
                        </router-link>
                        <button class="button ml-2 is-danger" @click="excluir(projeto.id)">
                            <span class="icon is-small">
                                <i class="fas fa-trash"></i>
                            </span>
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script lang="ts">
import { useStore } from '@/store';
import { EXCLUIR_PROJETO } from '@/store/tipo-mutacoes';
import { defineComponent, computed } from 'vue';
import { TipoNotificacao } from '@/interfaces/INotificacao';
import useNotificador from '@/hooks/notificador';


export default defineComponent({
    name: 'ListaPagina',
    methods: {
        excluir(id: string) {
            this.store.commit(EXCLUIR_PROJETO, id)
            this.notificar(TipoNotificacao.FALHA, 'Excluido!', 'O projeto foi deletado')
        }
    },
    setup() {
        const store = useStore()
        const { notificar } = useNotificador()
        return {
            projetos: computed(() => store.state.projetos),
            store,
            notificar
        }
    }
})
</script>