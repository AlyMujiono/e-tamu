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
            <h3>ID Kunjungan</h3>
            <p>Berikut adalah Id kunjungan anda</p>
            <div class="otp">
                <label for="otp">123456</label>
            </div>
            <br />
            <p>
                Dimohon untuk melihat video induction sebelum melakukan
                kunjungan
            </p>
            <a class="button" href="#e">Video induction</a>
            <p>
                Untuk cek status dan detail kunjungan silahkan
                <a href="a#">klik disini</a>
            </p>
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
    .otp {
        font-size: 50px;
        font-family: cursive;
        color: aqua;
    }
    .button {
        padding: 12px;
        width: 190px;
        cursor: pointer;
        background: #406aa8;
        color: white;
        transition: 0.5s ease;
        border-radius: 10px;
    }
    .button:hover {
        background: transparent;
        border: 2px solid #406aa8;
        box-shadow: 0 0 10px 0 #406aa8 inset, 0 0 10px 4px #406aa8;
    }
</style>
