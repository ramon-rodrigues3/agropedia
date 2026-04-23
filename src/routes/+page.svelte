<script lang="ts">
    // interface Planta {
    //     nome: string;
    //     tipo: string;
    // };

    import baseDados from '$lib/data.json';
    // type Planta = typeof baseDados[0];
    // const plantas = baseDados;
</script>

<h1>Agro Projeto</h1>
<p>Aqui neste site, você encontrará informações sobre o cultivo de diferentes culturas</p>

<section class="grid">
<h2>Plantas</h2>
  {#each baseDados as planta}
    <a href="/plantas/{planta.nome}">
        <div class="card">
            <h3>{planta.nome}</h3>
        </div>
    </a>
  {:else}
    <p>Nenhum dado encontrado.</p>
  {/each}
</section>

<style>
  .grid {
    display: grid;
    gap: 1rem;
  }
  .card {
    border: 1px solid #ccc;
    padding: 1rem;
    border-radius: 8px;
  }
</style>