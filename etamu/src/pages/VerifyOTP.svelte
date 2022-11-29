<script>
    import axios from 'axios';
    import Cookies from 'js-cookie';
    import IconQ from "../assets/img/Icon-Q.png";
    import IconX from "../assets/img/Icon-X.png";
    import IconV from "../assets/img/Icon-V.png";
    import TopNav from "../components/TopNav.svelte";
    let success = null;
    let OTP = '';
    let resendSuccess = null;

    async function resendOTP () {
        // api/v1/visits/otp/resend
        try {
            const OTPToken = Cookies.get("otp");
            const response = await axios.get("http://localhost:8000/api/v1/visits/otp/resend", {
                headers: {
                    Authorization : `OTP ${OTPToken}`
                },
            });
            console.log(response.data);
            if (response.data.success === true) {
                resendSuccess = true;
            }

        } catch (error) {
            console.log(error)    
        }
    }
    async function SubmitOTP () {
        try {
            const OTPToken = Cookies.get("otp")
            const response = await axios({
            method: 'post',
            url: 'http://localhost:8000/api/v1/visit/verify',
            data : {otp_token : OTP},
            headers: {"Authorization" : `OTP ${OTPToken}`},
             })
            console.log(response);
            success = response.data.success;
        } catch (error) {
            console.log(error);
            success = false;
        }
    }
</script>

<TopNav title="Konfirmasi Kode OTP" />
<div class="container">
    {#if success === true}
    <div class="form-container">
        <img class="img" src={IconV} alt="Berhasil" />
        <h3>BERHASIL</h3>
        <p>Kode OTP berhasil di konfirmasi.</p>
        <div class="button-container">
            <button on:click={() => {window.location.href = "/visitinfo"}}
            >OK</button>
        </div>
    </div>
    {:else if success === false}
    <div class="form-container">
        <img class="img" src={IconX} alt="Gagal" />
        <h3>GAGAL</h3>
        <p>Kode OTP salah.</p>
        <div class="button-container">
            <button on:click={() => {window.location.href = "/registervisit/verify"}}
            >Coba Lagi</button>
        </div>
        
    </div>
    {:else}   
        <div class="form-container">
            <img class="img" src={IconQ} alt="Isi OTP" />
            <h3>Masukan Kode OTP</h3>
            <p>Cek email anda untuk kode OTP.</p>
            <div class="input-container">
                <input id="opt_token" type="text" bind:value={OTP}>    
            </div>
            <div class="button-container">
                <button on:click={SubmitOTP} disabled={OTP == ''}>Verify</button>
            </div>
            {#if resendSuccess === true}
            <p>kode OTP telah dikirim ulang!</p>
            {/if}
            <p>Tidak menerima kode? <a href="#a" on:click|preventDefault={async () => {
                await resendOTP()
            }}> Kirim ulang!</a></p>
        </div>
    {/if}
</div>

<style>
    .container {
        box-sizing: border-box;

        /* Auto layout */
        
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 20px;
        
        width: 55%;
        height: 75%;
        margin-top: 30px;
        margin-left: auto;
        margin-right: auto;
        
        /* Black */
        
        background: #1A1A1A;
        border: 1px solid #FFFFFF;
        /* Shadow */
        
        box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.25), 0px 12px 20px rgba(0, 0, 0, 0.15);
        border-radius: 8px;
    }
    .form-container {
        margin: auto;
    }
    h3 {
        color: white;
    }
    p {
        color: white;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        width: 260px;
        margin-left: auto;
        margin-right: auto;
        gap: 5px;
        margin-bottom: 0.2em;
    }
    input[type="text"] {
        display: block;
        width: 90%;
        height: 90%;
        margin: 15px auto;
        background: #fff;
        border: 0px;
        padding: 5px;
        font-size: 16px;
        border: 2px solid #fff;
        transition: all 0.3s ease;
        border-radius: 5px;
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
        text-align: center; 
    }

    input[type="text"]:focus {
        border: 2px solid #1abc9d;
    }
    button {
        box-sizing: border-box;

        /* Auto layout */        
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        padding: 8px 16px;
        gap: 8px;
        
        width: 260px;
        height: 40px;
        
        /* White */        
        border: 1px solid #FFFFFF;
        border-radius: 4px;
        
        /* Inside auto layout */        
        flex: none;
        order: 1;
        flex-grow: 0;
        background:  #1A1A1A;
        color: white;
    }

    button:hover {
        background: #FFFFFF;
        color: black;
    }

</style>