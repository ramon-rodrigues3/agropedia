<script lang="ts">
    import { page } from '$app/stores';
    import baseDados from '$lib/prototipo.json';

    // 1. Pegamos o nome que veio da URL
    const nomeUrl = $page.params.nome;

    // 2. Procuramos a planta correspondente no JSON
    const planta = baseDados.find(p => p.nome === nomeUrl);
</script>

<table>
    <tbody>
        <tr>
            <td><img src="https://www.infoescola.com/wp-content/uploads/2011/01/tomate_345187874.jpg" alt="tomate" width="200"></td>
        </tr>
        <tr>
            <td>Nome</td>
            <td>{planta?.nome}</td>
        </tr>
        <tr>
            <td>Nome Científico</td>
            <td>{planta?.nome_cientifico}</td>
        </tr>
        <tr>
            <td>Família</td>
            <td>{planta?.familia}</td>
        </tr>
    </tbody>
</table>

<h2>Informações de Plantio</h2>
<table>
    <tbody>
    {#each Object.entries(planta?.info_cultivo || {}) as [chave, valor]}
      <tr>
            <td>{chave}</td>
            <td>{valor}</td>
            
        </tr>  
    {/each}
        
        <tr>
            <!-- "luminosidade",
            "solo",
            "temperatura_ideal",
            "umidade_do_ar",
            "rega",
            "epoca_de_plantio",
            "profundidade_da_semente",
            "espacamento",
            "adubacao",
            "poda",
            "tempo_de_germinacao",
            "ciclo_total",
            "colheita",
            "possíveis ameaças?"-->
        </tr>
    </tbody>
</table>
<p>Fonte: Embrapa</p>

<h2>Informações nutricionais</h2>

<p>Valores por 100g</p>
<table>
    <tbody>
        {#each Object.entries(planta?.info_nutricionais || {})  as [chave, valor]}
            <tr>
                <td>{chave}</td>
                <td>{valor}</td>
            </tr> 
        {/each}
    </tbody>
</table>

<p>Fonte: Tabela Brasileira de Composição de Alimentos (TBCA) </p>