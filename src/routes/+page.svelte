<h1>Clear-ass MUD</h1>

Search: <input type="text" bind:value={searchTerm}>

<h2>{results.length} items matching: {searchTerm}</h2>
<table>
    <tr><th>Name</th><th>material</th></tr>
    {#each results as item}
        <tr>
            <td>{item.name}</td>
            <td>{item.type}</td>
            <td>{item.material}</td>
            <td>{item.flags}</td>
            <td>{item.HELD_BY}</td>
            <td>{item.SLOT}</td>
        </tr>
    {/each}
</table>

<script>
    import { items } from '../lib/items.js';
    let searchTerm = '';

    $: results = searchTerm == '' ? items : items.filter(doesItemMatch);

    function doesItemMatch(item) {
        return item.name.includes(searchTerm)
            || item.type.includes(searchTerm)
            || item.material.includes(searchTerm)
            || item.flags.includes(searchTerm)
            || item.HELD_BY?.includes(searchTerm)
            || item.SLOT?.includes(searchTerm);
    }
</script>