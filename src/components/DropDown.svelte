<script>
    import Day from './Day.svelte';
    export let value;
    export let view;
</script>
<style>
div {
    height: 224px;
    width: 224px;
}
</style>
<div>
<Day {value} on:input/>
</div>