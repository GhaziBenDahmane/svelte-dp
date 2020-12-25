<script>
    import dayjs from 'dayjs'
    import weekday from 'dayjs/plugin/weekday';
    import DropDown from './DropDown.svelte';

    dayjs.extend(weekday);

    export let dateTime = dayjs();

    function input(event) {
        dateTime = event.detail;
    }
</script>
<p>
<input value={dateTime}/>
<DropDown value={dateTime} on:input={input}/>
</p>