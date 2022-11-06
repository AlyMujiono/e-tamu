<script>
    import axios from 'axios';
    import Cookies from 'js-cookie';
    let success = null;
    let OTP = '';

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

<div class="container">
    {#if success === true}
    <div class="form-container">
        <h1>BERHASIL</h1>
    </div>
    {:else if success === false}
    <div class="form-container">
        <h1>GAGAL</h1>
    </div>
    {:else}   
        <div class="form-container">
            <div class="input-container">
                <label for="opt_token">Kode OTP</label>
                <input id="opt_token" type="text" bind:value={OTP}>    
            </div>
            <div class="button-container">
                <button on:click={SubmitOTP} disabled={OTP == ''}>Login</button>
            </div>
        </div>
    {/if}
</div>