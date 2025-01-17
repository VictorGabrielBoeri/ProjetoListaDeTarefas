<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <div>
            <button class="button mr-3" @click="iniciar" :disabled="cronometroRodando">
                <span class="icon">
                    <i class="fas fa-play"></i>
                </span>
                <span>Iniciar</span>
            </button>
            <button class="button" @click="finalizar" :disabled="!cronometroRodando">
                <span class="icon">
                    <i class="fas fa-stop"></i>
                </span>
                <span>Parar</span>
            </button>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Cronometro from './Cronometro.vue';

export default defineComponent({
    name: 'TemporizadorComponente',
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Cronometro
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
        }
    },
    methods: {
        iniciar() {
            // Começar a contagem
            // 1 Segundo == 1000 ms
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1;
            }, 1000)
        },

        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>