<script lang="ts">
	import logo from '$lib/assets/logo.png'
    import baseDados from '$lib/data.json';

    
    let busca = $state('');
    let mostrarResultados = $state(false);

    let resultadosFiltrados = $derived(
        busca.length > 1 
            ? baseDados.filter(p => p.nome.toLowerCase().includes(busca.toLowerCase())).slice(0, 5) 
            : []
    );

    function limparBusca() {
        busca = '';
        mostrarResultados = false;
    }

    let { children } = $props();
</script>

<header class="main-header">
    <div class="nav-container">
        <a href="/" class="brand" onclick={limparBusca}>
            <img src="{logo}" alt="Logo Agropédia" class="logo">
            <span class="brand-name">Agropédia</span>
        </a>

        <nav class="links">
            <a href="/">Home</a>
            <a href="/sobre">Sobre</a>
        </nav>

        <div class="search-wrapper">
            <div class="search-field">
                <input 
                    type="text" 
                    placeholder="Buscar cultura..." 
                    bind:value={busca}
                    onfocus={() => mostrarResultados = true}
                >
                <span class="search-icon">🔍</span>
            </div>

            {#if busca.length > 1 && mostrarResultados}
                <div class="search-results">
                    {#each resultadosFiltrados as item}
                        <a href="/plantas/{item.nome}" onclick={limparBusca} class="result-item">
                            <span class="item-nome">{item.nome}</span>
                            <span class="item-familia">{item.familia || 'Ver detalhes'}</span>
                        </a>
                    {:else}
                        <div class="no-result">Nenhum cultivo encontrado</div>
                    {/each}
                </div>
            {/if}
        </div>
    </div>
</header>

<main>
    {@render children()}
</main>

<style>
    .main-header {
        background-color: #2e7d32;
        border-bottom: 4px solid #000;
        padding: 10px 20px;
        position: sticky;
        top: 0;
        z-index: 1000;
        color: white;
    }

    .nav-container {
        max-width: 1200px;
        margin: 0 auto;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 20px;
    }

    .brand {
        display: flex;
        align-items: center;
        gap: 12px;
        text-decoration: none;
        color: #ffeb3b;
    }

    .logo {
        width: 40px;
        height: 40px;
        border: 2px solid #000;
        border-radius: 4px;
        background: white;
    }

    .brand-name {
        font-size: 1.5rem;
        font-weight: bold;
        text-transform: uppercase;
        letter-spacing: 1px;
        text-shadow: 2px 2px #000;
    }

    .links {
        display: flex;
        gap: 20px;
    }

    .links a {
        color: white;
        text-decoration: none;
        font-weight: 500;
        transition: color 0.2s;
    }

    .links a:hover {
        color: #ffeb3b;
    }

    .search-wrapper {
        position: relative;
        flex-grow: 1;
        max-width: 400px;
    }

    .search-field {
        display: flex;
        align-items: center;
        background: white;
        border: 2px solid #000;
        border-radius: 4px;
        padding: 5px 10px;
    }

    .search-field input {
        border: none;
        outline: none;
        width: 100%;
        padding: 5px;
        font-size: 1rem;
    }

    .search-icon {
        color: #666;
    }

    .search-results {
        position: absolute;
        top: 110%;
        left: 0;
        right: 0;
        background-color: #795548;
        border: 2px solid #000;
        border-radius: 4px;
        box-shadow: 6px 6px 0 rgba(0,0,0,0.2);
        overflow: hidden;
    }

    .result-item {
        display: flex;
        justify-content: space-between;
        padding: 12px 15px;
        text-decoration: none;
        color: white;
        border-bottom: 1px solid rgba(0,0,0,0.2);
        transition: background 0.2s;
    }

    .result-item:hover {
        background-color: #5d4037;
    }

    .item-nome {
        font-weight: bold;
        color: #ffeb3b;
    }

    .item-familia {
        font-size: 0.8rem;
        font-style: italic;
        opacity: 0.8;
    }

    .no-result {
        padding: 15px;
        text-align: center;
        font-style: italic;
        background: #6d4c41;
    }

    @media (max-width: 768px) {
        .brand-name, .links {
            display: none;
        }
    }
</style>