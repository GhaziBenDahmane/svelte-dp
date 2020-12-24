<script>
    import Day from './Day.svelte';
    export let value;
    export let view;
    let formattedDate;
</script>
<style>
div {
    background-color: aqua;
    height: 500px;
    width: 700px;
}
</style>
<div>
<Day {value} on:input/>
</div>