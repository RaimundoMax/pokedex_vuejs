<script setup>
// Importação dos elementos vue-router
import { RouterLink, RouterView } from 'vue-router'

// Importação do Bootstrap
import 'bootstrap/dist/css/bootstrap.min.css'

//Importar estilo css
import './complementos/estilos.css';

// Importar componente de navegação
import BarraNavegacao from './componentes/BarraNavegacao.vue';
</script>




<template>
  <!-- BARRA DE NAVEGAÇÃO -->
  <BarraNavegacao/>
  <nav>
    
    
    
  </nav>
    
<!-- vISUALIZAR CONTEUDO AS PAGINAS-->
  <RouterView />
</template>

