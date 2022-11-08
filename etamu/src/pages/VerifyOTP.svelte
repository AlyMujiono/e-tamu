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
            <fieldset class='number-code'>
                <legend>Kode OTP</legend>
                    <div class="input-container">
                        <input id="opt_token" type="text" bind:value={OTP}>    
                    </div>
            </fieldset>
            <div class="button-container">
                <button on:click={SubmitOTP} disabled={OTP == ''}>Login</button>
            </div>
        </div>
    {/if}
</div>

<style>
    .form-container {
        width: 500px;
        background: #edeff1;
        margin: 0px auto;
        padding-top: 20px;
        padding-bottom: 20px;
        border-radius: 10px;
        -moz-border-radius: 10px;
        -webkit-border-radius: 10px;
    }
    fieldset {
        display: block;
        margin-inline-start: 2px;
        margin-inline-end: 2px;
        padding-block-start: 0.35em;
        padding-inline-start: 0.75em;
        padding-inline-end: 0.75em;
        padding-block-end: 0.625em;
        min-inline-size: min-content;
        border-width: 2px;
        border-style: groove;
        border-color: rgb(192, 192, 192);
        border-image: initial;
        margin-left: auto;
        margin-right: auto;
        width: 80%;
    }
    legend {
        display: block;
        padding-inline-start: 2px;
        padding-inline-end: 2px;
        border-width: initial;
        border-style: none;
        border-color: initial;
        border-image: initial;
        font-weight: bold;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        width: 80%;
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
        display: block;
        background: #1abc9d;
        width: 314px;
        padding: 12px;
        cursor: pointer;
        color: #fff;
        border: 0px;
        margin: auto;
        margin-top: 20px;
        border-radius: 5px;
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
        font-size: 17px;
        transition: all 0.3s ease;
    }

    button:hover {
        background: #09cca6;
    }

</style>