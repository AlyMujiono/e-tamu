<script>
    import { Link } from "svelte-routing";
    import axios from "axios";
    import Cookies from "js-cookie";
    import Logo from "../assets/img/logolabinta.png";
</script>

<div class="container">
    <div class="form-container">
        <div class="logo">
            <img src={Logo} alt="Logo labinta" />
            <h2>PT. Sugar Labinta</h2>
        </div>
        <div>
            <h3>Kunjungan Baru</h3>
            <p>Anda menerima permintaan kunjungan atas nama</p>
            <label for="name" class="name">Albert Einstein</label>
            <br />
            <p>Dengan Id kunjungan</p>
            <div class="id">
                <label for="id">123456</label>
            </div>
            <br />
            <p>Silahkan periksa detail kunjungan dari dashboard anda</p>
        </div>
    </div>
</div>

<style>
    .form-container {
        position: absolute;
        width: 90%;
        height: 85%;
        left: 5%;
        right: 5%;
        top: 50px;
        background: #1a1a1a;
    }
    .logo {
        height: 20%;
        align-items: center;
        margin-top: 50px;
    }
    img {
        border-radius: 50%;
        width: 100px;
        position: relative;
    }
    h2 {
        color: white;
        margin-top: 0px;
        font-size: 20px;
    }
    h3 {
        color: white;
        margin-top: 50px;
    }
    p {
        color: white;
        margin-top: 20px;
    }
    .id {
        font-size: 50px;
        font-family: cursive;
        color: aqua;
    }
    .name {
        font-size: 30px;
        font-family: "Courier New", Courier, monospace;
        color: yellow;
    }
</style>
