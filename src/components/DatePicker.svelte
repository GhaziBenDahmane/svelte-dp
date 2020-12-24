<script>
    import dayjs from 'dayjs'
    import DropDown from './DropDown.svelte';
    export let dateTime = dayjs();

    function inputHandler(date) {
        console.log(date)
        dateTime = date.detail;
    }
</script>
<p>
<input value={dateTime}/>
<DropDown value={dateTime} on:input={inputHandler}/>
</p>