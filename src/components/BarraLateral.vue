<template>
    <header>
        <h1>
            <!-- <img src="../assets/logo.png" alt=""> -->
            <i class="fa-solid fa-laptop-code icone"></i>
        </h1>
        <button class="button" @click="alterarTema">
            {{ textoBotao }}
        </button>
        <nav class="panel shadow-none mt-5">
            <ul>
                <li>
                    <router-link class="link" to="/">
                        <i class="fas fa-tasks"></i>
                        Tarefas
                    </router-link>
                </li>

                <li>
                    <router-link class="link" to="/projetos">
                        <i class="fas fa-project-diagram"></i>
                        Projetos
                    </router-link>
                </li>
            </ul>
        </nav>

        <div class="is-flex">
            <a class="mr-5" href="https://github.com/VictorGabrielBoeri" target="_blank">
                <i class="fa-brands fa-github icone-sm"></i>
            </a>

            <a href="https://instagram.com/victor.gabriel.boeri" target="_blank">
                <i class="fa-brands fa-instagram icone-sm"></i>
            </a>
        </div>
    </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'BarraLateral',
    emits: ['aoTemaAlterado'],
    data() {
        return {
            modoEscuroAtivo: false
        }
    },
    computed: {
        textoBotao() {
            if (this.modoEscuroAtivo) {
                return 'Desativar modo escuro'
            }
            return 'Ativar modo escuro'
        }
    },
    methods: {
        alterarTema() {
            this.modoEscuroAtivo = !this.modoEscuroAtivo
            this.$emit('aoTemaAlterado', this.modoEscuroAtivo)
        }
    }
})
</script>

<style scoped>
header {
    padding: 1rem;
    background: #35495e;
    width: 100%;
    height: 100vh;
    text-align: center;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}

.panel li {
    margin: 8px 0;
    text-align: start;
}

.link {
    color: #fff;
}

.link:hover {
    color: #FAF0CA;
}

.link.router-link-active {
    color: #FAF0CA;
}

.shadow-none {
    box-shadow: none;
}

.icone {
    font-size: 110px;
    color: white;
    margin-bottom: 50px;
}

.icone-sm {
    display: flex;
    justify-content: left;
    font-size: 35px;
    color: white;
}
</style>