
<script>
    import Logo from "../assets/img/Logo.png"

    export let title = '';
</script>

<div class="main-container">
    <div class="topnav">
        <img src="{Logo}" alt="Logo labinta">
        <h4>{title}</h4>
    </div>
</div>

<style>
    .topnav {
        top: 0;
        left: 0;
        display :block;
        display: flex;
        align-self: flex-start;
        align-items: center;
        background-color: #1A1A1A;
        width: 100%;
    }
    .topnav img {
        margin-right: 10vh;
    }
</style>