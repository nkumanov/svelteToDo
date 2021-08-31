<script>
    import { HsvPicker } from "svelte-color-picker";
    import { createEventDispatcher } from "svelte";
    export let parseColor;
    let colorChange = createEventDispatcher();

    function colorCallback(rgba) {
        parseColor = Object.values(rgba.detail).join(", ");
        colorChange("colorChange", parseColor);
    }
</script>

<section>
    <HsvPicker on:colorChange={colorCallback} startColor={"#ffffff"} />
</section>

<style>
</style>
