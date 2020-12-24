<script>
import { createEventDispatcher } from "svelte";


    // import dayjs from 'dayjs';
    export let value;
    $: offset = value.startOf('month').startOf('week').format('DD');
    $: days = [...new Array(35).keys()].map(d => d - parseInt(value.subtract(offset, 'day').format('DD')));

    const dispatch = createEventDispatcher();
    function click(day) {
        dispatch('input', day);
    }
    $: console.log({days,value,offset})
</script>
<style>
div {
    width: 98px;
    height: 98px;
    display: inline-block;
    border: solid red 1px;
}
</style>
{#each days as day}
    <div on:click={()=>click(value.add(day, 'day'))}>
        {value.add(day, 'day').format('DD')}
    </div>
{/each}
    
