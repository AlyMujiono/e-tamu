<script>
    import Logo from "../assets/img/labinta_logo.png";

    export let title = "";
</script>

<div class="main-container">
    <div class="topnav">
        <img class="img" src={Logo} alt="Logo labinta" />
        <h4 class="name">{title}</h4>
    </div>
</div>

<style>
    .topnav {
        top: 0;
        left: 0;
        display: block;
        display: flex;
        align-self: flex-start;
        align-items: center;
        background-color: #1a1a1a;
        width: 100%;
    }
    .topnav img {
        margin-right: 10vh;
    }
    .name {
        color: white;
    }
    .img {
        width: 100px;
    }
</style>
