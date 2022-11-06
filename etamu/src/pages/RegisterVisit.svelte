<script> 
    import axios from 'axios';
    import Cookies from 'js-cookie'
    let userEmail = '';
    let userPassword = '';

    async function Login() {
        try {
            const response = await axios.post("http://localhost:8000/api/v1/login", {
                user_email : userEmail,
                user_password : userPassword
            });
            const res = response.data;
            var expTime = new Date(new Date().getTime() + 60 * 60 * 1000);

            Cookies.set("token", res.data.token, {
                expires: expTime
            })
        } catch (err) {
            console.log("Error : ", err)
        }
    }

</script>

<div class="login-container">
    <div class="input-container">
        <label for="user_email">Email</label>
        <input id="user_email" type="text" bind:value={userEmail}>
    </div>
    <div class="input-container">
        <label for="user_password">Password</label>
        <input id="user_password" type="text" bind:value={userPassword}>    
    </div>
    <div class="button-container">
        <button on:click={Login} disabled={userEmail == '' || userPassword == ''}>Login</button>
    </div>
</div>


<style>

</style>
