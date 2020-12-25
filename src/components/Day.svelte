<script>
    import { createEventDispatcher } from "svelte";

    export let value;
    $: offset = value.date(1).weekday() - 1;
    $: days = [...new Array(42).keys()].map(d => d - parseInt(value.add(offset, 'day').format('D')));
    $: console.log(offset, days);
    const dispatch = createEventDispatcher();
    function click(day) {
        dispatch('input', day);
    }
    function dayClass(date, day) {
        if (!day) return 'cell day today';
        if(date.month() !== date.add(day, 'day').month()) return 'cell day outside';
        return 'cell day inside';
    }
</script>
<style>
.cell {
    width: 30px;
    height: 30px;
    display: inline-block;
}
.day {
    cursor: pointer;
}
.outside {
    background-color: white;
}
.inside {
    background-color: blue;
}
.today {
    background-color: red;
}
.label {
    background-color: gray;
}
</style>
{#each days.slice(0, 7) as day}
    <div class="cell label">
        {value.add(day, 'day').format('ddd')}
    </div>
{/each}
{#each days as day}
    <div on:click={()=>click(value.add(day, 'day'))} class={dayClass(value, day)}>
        {value.add(day, 'day').format('D')}
    </div>
{/each}
    
