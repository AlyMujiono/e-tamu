<script>
    import axios from "axios";
    import Cookies from "js-cookie";
    import Logo from "../assets/img/logolabinta.png";
</script>

<div class="container">
    <div class="form-container">
        <div class="logo">
            <img src={Logo} alt="Logo labinta" />
            <h2>PT. Sugar Labinta</h2>
            <h3>Kode OTP</h3>
            <p>Berikut adalah kode OTP Verivikasi anda</p>
            <div class="otp">
                <label for="otp">123456</label>
            </div>
            <p>Silahkan masukan kode OTP anda di halaman verifikasi E-mail</p>
            <a href="#3">Klik Disni</a>
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
    }
    p {
        color: white;
    }
    .otp {
        font-size: 50px;
        font-family: cursive;
        color: aqua;
    }
</style>
