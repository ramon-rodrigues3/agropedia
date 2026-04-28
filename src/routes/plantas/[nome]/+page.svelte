<script lang="ts">
    import { page } from '$app/stores';
    import baseDados from '$lib/data.json';

    // 1. Pegamos o nome que veio da URL
    const nomeUrl = $page.params.nome;

    // 2. Procuramos a planta correspondente no JSON
    const planta = baseDados.find(p => p.nome === nomeUrl);
</script>

{#if planta}
    <h1>{planta.nome}</h1>
    <p>Tipo: {planta.tipo}</p>
    <a href="/">← Voltar para a lista</a>
{:else}
    <h1>Planta não encontrada</h1>
    <a href="/">Voltar para a lista</a>
{/if}

<h2>Informações nutricionais</h2>

<h2>Informações de Plantio</h2>

<h2>Orígem?? </h2>