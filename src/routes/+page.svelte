<script lang="ts">
    import baseDados from '$lib/data.json';
    
    let itensVisiveis = $state(12);
    
    function carregarMais() {
        itensVisiveis += 12;
    }

    let plantasExibidas = $derived(baseDados.slice(0, itensVisiveis));
    let temMaisParaMostrar = $derived(itensVisiveis < baseDados.length);
</script>

<div class="container">
    <header class="hero">
        <h1>Agropédia</h1>
        <p>Explore o guia completo para cultivo e nutrição. Aprenda a plantar com técnica e colher com saúde.</p>
    </header>

    <section class="catalogo">
        <h2>Catálogo de Culturas</h2>
        
        <div class="grid">
            {#each plantasExibidas as planta}
                <a href="/plantas/{planta.nome}" class="card-link">
                    <article class="card">
                        <div class="img-container">
                            <img src={planta.imagem.url || 'https://via.placeholder.com/150?text=Planta'} alt={planta.nome}>
                        </div>
                        <div class="card-content">
                            <h3>{planta.nome}</h3>
                            <p class="cientifico"><em>{planta.nome_cientifico || ''}</em></p>
                        </div>
                    </article>
                </a>
            {:else}
                <p class="vazio">Nenhuma planta encontrada no pomar...</p>
            {/each}
        </div>

        {#if temMaisParaMostrar}
            <div class="acoes">
                <button onclick={carregarMais} class="btn-ver-mais">
                    Ver Mais Plantas
                </button>
            </div>
        {/if}
    </section>
</div>

<style>
    :global(body) {
        background-color: #f4f1ea;
        font-family: 'Segoe UI', sans-serif;
        margin: 0;
        color: #2c2c2c;
    }

    .container {
        max-width: 1000px;
        margin: 0 auto;
        padding: 20px;
    }

    .hero {
        text-align: center;
        padding: 40px 20px;
        background-color: #2e7d32;
        color: white;
        border-radius: 12px;
        margin-bottom: 30px;
        border: 3px solid #000;
    }

    .hero h1 {
        margin: 0;
        font-size: 3rem;
        color: #ffeb3b;
        text-shadow: 2px 2px #000;
    }

    h2 {
        color: #5d4037;
        border-bottom: 3px solid #fbc02d;
        display: inline-block;
        margin-bottom: 20px;
    }

    .grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
        gap: 20px;
    }

    .card-link {
        text-decoration: none;
        color: inherit;
    }

    .card {
        background-color: #795548;
        border: 2px solid #000;
        border-radius: 8px;
        overflow: hidden;
        transition: transform 0.2s, box-shadow 0.2s;
        height: 100%;
        display: flex;
        flex-direction: column;
    }

    .card:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 0 #000;
        border-color: #000;
    }

    .img-container {
        height: 150px;
        background-color: #fff;
        border-bottom: 2px solid #000;
    }

    .img-container img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .card-content {
        padding: 15px;
        color: white;
        flex-grow: 1;
    }

    .tag {
        background-color: #fbc02d;
        color: #000;
        font-size: 0.7rem;
        padding: 2px 8px;
        border-radius: 4px;
        font-weight: bold;
        text-transform: uppercase;
    }

    h3 {
        margin: 10px 0 5px 0;
        text-transform: capitalize;
    }

    .cientifico {
        font-size: 0.85rem;
        opacity: 0.9;
        margin: 0;
    }

    .acoes {
        display: flex;
        justify-content: center;
        margin-top: 40px;
    }

    .btn-ver-mais {
        background-color: #fbc02d;
        color: #000;
        border: 2px solid #000;
        padding: 15px 40px;
        font-weight: bold;
        font-size: 1.1rem;
        cursor: pointer;
        border-radius: 4px;
        box-shadow: 4px 4px 0 #000;
    }

    .btn-ver-mais:hover {
        background-color: #ffeb3b;
        transform: translate(-2px, -2px);
        box-shadow: 6px 6px 0 #000;
    }

    .btn-ver-mais:active {
        transform: translate(2px, 2px);
        box-shadow: 0px 0px 0 #000;
    }

    .vazio {
        text-align: center;
        grid-column: 1 / -1;
        padding: 40px;
        font-style: italic;
    }
</style>