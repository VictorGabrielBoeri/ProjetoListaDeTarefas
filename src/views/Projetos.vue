<template>
    <section class="projetos">
        <h1 class="title title-modo-escuro">Projetos</h1>
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
        <table class="table is-fullwidth">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nome</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="projeto in projetos" :key="projeto.id">
                    <td>{{ projeto.id }}</td>
                    <td>{{ projeto.nome }}</td>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script lang="ts">
import { useStore } from '@/store';
import { defineComponent } from 'vue';
import { computed } from 'vue';


export default defineComponent({
    name: 'PaginaProjetos',
    data() {
        return {
            nomeDoProjeto: ""
        }
    },
    methods: {
        salvar() {
            this.store.commit('ADICIONA_PROJETO', this.nomeDoProjeto)
            this.nomeDoProjeto = ''
        },
    },
    setup () {
        const store = useStore()
        return {
            store,
            projetos: computed(() => store.state.projetos)
        }
    }
})
</script>

<style scoped>
.projetos {
    padding: 1.25rem;
}

.title-modo-escuro {
    color: var(--texto-primario);
}
</style>