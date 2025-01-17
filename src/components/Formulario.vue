<template>
    <div class="box formulario" style="border: none; box-shadow: none; border-radius: inherit;">
        <div class="columns">
            <div class="column is-8" role="form" arial-label="Formulario de criação para uma tarefa">
                <div class="control">
                    <input type="text" class="input is-normal" placeholder="Qual terefa deseja iniciar" v-model="descricao" />
                </div>
            </div>
            <div class="column">
                <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Temporizador from './Temporizador.vue';

export default defineComponent({
    name: 'FormularioComponente',
    emits: ['aoSalvarTarefa'],
    components: {
        Temporizador
    },
    data() {
        return {
            descricao: '',
        }
    },
    methods: {
        finalizarTarefa (tempoDecorrido: number) : void {
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            })
            this.descricao = ''
        }
    }
})
</script>

<style>
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>