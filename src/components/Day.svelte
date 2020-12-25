<script>
    import { createEventDispatcher } from "svelte";
    import dayjs from "dayjs";
    import DropDown from "./DropDown.svelte";

    export let value;
    $: firstDay = value.startOf("month");
    $: firstDayOfCalendar = firstDay.subtract(firstDay.weekday() || 7, "day");
    $: days = [...new Array(42).keys()].map((i) =>
        firstDayOfCalendar.add(i, "day")
    );
    const dispatch = createEventDispatcher();
    function click(day) {
        dispatch("input", day);
    }
    function dayClass(day) {
        if (day.isSame(value)) return "cell day today";
        if (day.month() === value.month()) return "cell day inside";
        return "cell day outside";
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

{#each [...new Array(7).keys()] as day}
    <div class="cell label">
        {firstDayOfCalendar.add(day, 'day').format('ddd')}
    </div>
{/each}
{#each days as day}
    <div on:click={() => click(day)} class={dayClass(day)}>
        {day.format('D')}
    </div>
{/each}
