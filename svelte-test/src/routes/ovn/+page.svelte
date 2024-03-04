<script>
    import "../../app.css";
    let temp = 0;
</script>

<div class="bg-">
    <p>{temp}</p>

    <button on:click={() => temp + 1 <= 240 ? temp += 1 : 240}>Pluss</button>
    <button on:click={() => temp - 1 >= 0 ? temp -= 1 : 0}>Minus</button>
</div> 

<p>test</p>