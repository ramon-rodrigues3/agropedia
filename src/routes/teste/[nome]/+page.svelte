<script lang="ts">
    import { page } from '$app/stores';
    import baseDados from '$lib/data.json';

    const nomeUrl = $page.params.nome;
    const planta = baseDados.find(p => p.nome === nomeUrl);
</script>

<div class="container">
    <div class="header-section">
        <img src="https://www.infoescola.com/wp-content/uploads/2011/01/tomate_345187874.jpg" alt="tomate" class="planta-img">
        <h1>{planta?.nome || 'Planta'}</h1>
        <p class="fonte-imagem">Fonte da imagem: InfoEscola</p>
    </div>

    <section>
        <table>
            <thead>
                <tr>
                    <th colspan="2">Dados Gerais</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><strong>Nome Científico</strong></td>
                    <td>{planta?.nome_cientifico}</td>
                </tr>
                <tr>
                    <td><strong>Família</strong></td>
                    <td>{planta?.familia}</td>
                </tr>
            </tbody>
        </table>
    </section>

    <section>
        <h2>Informações de Plantio</h2>
        <table>
            <thead>
                <tr>
                    <th>Atributo</th>
                    <th>Recomendação</th>
                </tr>
            </thead>
            <tbody>
                {#each Object.entries(planta?.info_cultivo || {}) as [chave, valor]}
                    <tr>
                        <td class="chave">{chave.replace(/_/g, ' ')}</td>
                        <td>{valor}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
        <p class="fonte">Fonte: Embrapa</p>
    </section>

    <section>
        <h2>Informações Nutricionais</h2>
        <p class="subtitulo">Valores aproximados por 100g</p>
        <table>
            <thead>
                <tr>
                    <th>Nutriente</th>
                    <th>Quantidade</th>
                </tr>
            </thead>
            <tbody>
                {#each Object.entries(planta?.info_nutricionais || {}) as [chave, valor]}
                    <tr>
                        <td class="chave">{chave}</td>
                        <td>{valor}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
        <p class="fonte">Fonte: TBCA</p>
    </section>
</div>

<style>
    :global(body) {
        background-color: #f4f1ea; /* Branco levemente creme */
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        color: #2c2c2c; /* Preto suave */
        margin: 0;
        padding: 20px;
    }

    .container {
        max-width: 800px;
        margin: 0 auto;
        background-color: white;
        padding: 30px;
        border-radius: 12px;
        box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }

    .header-section {
        text-align: center;
        border-bottom: 3px solid #4CAF50; /* Verde */
        margin-bottom: 30px;
        padding-bottom: 20px;
    }

    .planta-img {
        width: 250px;
        height: auto;
        border-radius: 50%;
        border: 4px solid #5d4037; /* Marrom */
        margin-bottom: 15px;
    }

    h1 {
        color: #2e7d32; /* Verde escuro */
        margin: 0;
        text-transform: capitalize;
    }

    h2 {
        color: #5d4037; /* Marrom */
        border-left: 5px solid #ffeb3b; /* Amarelo */
        padding-left: 10px;
        margin-top: 40px;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 10px;
        background-color: #795548; /* Marrom base da tabela */
        color: white;
        border: 2px solid #000; /* Contorno preto */
    }

    th {
        background-color: #fbc02d; /* Amarelo escuro/Ouro */
        color: #000; /* Texto preto no cabeçalho */
        padding: 12px;
        text-align: left;
        border-bottom: 2px solid #000;
        text-transform: uppercase;
        font-size: 0.9em;
    }

    td {
        padding: 10px 15px;
        border: 1px solid rgba(0,0,0,0.2);
    }

    tr:nth-child(even) {
        background-color: #6d4c41; /* Marrom levemente diferente para listras */
    }

    .chave {
        font-weight: bold;
        text-transform: capitalize;
        width: 40%;
    }

    .fonte {
        font-size: 0.8em;
        font-style: italic;
        color: #666;
        margin-top: 5px;
    }

    .subtitulo {
        font-size: 0.9em;
        margin-bottom: 5px;
    }
    .image-wrapper {
        margin-bottom: 15px;
    }

    .planta-img {
        width: 250px;
        height: 250px;
        object-fit: cover; /* Garante que a imagem preencha o círculo sem distorcer */
        border-radius: 50%;
        border: 4px solid #5d4037; /* Marrom */
        margin-bottom: 5px;
    }

    .fonte-imagem {
        font-size: 0.75em;
        color: #888;
        margin: 0;
        font-style: italic;
    }

    /* Estilos das Tabelas (conforme solicitado: Fundo marrom, contorno preto, cabeçalho amarelo) */
    table {
        width: 100%;
        border-collapse: collapse;
        background-color: #795548; /* Marrom */
        color: white;
        border: 2px solid #000; /* Contorno preto */
        margin-bottom: 10px;
    }

    th {
        background-color: #fbc02d; /* Amarelo */
        color: #000; /* Texto preto */
        padding: 12px;
        border-bottom: 2px solid #000;
        text-transform: uppercase;
    }

    td {
        padding: 10px;
        border: 1px solid #000; /* Divisórias internas em preto */
    }

    tr:nth-child(even) {
        background-color: #6d4c41; /* Variação de marrom para leitura */
    }

    /* Reaproveitando classes gerais */
    .fonte {
        font-size: 0.8em;
        color: #5d4037;
        margin-bottom: 20px;
    }
</style>