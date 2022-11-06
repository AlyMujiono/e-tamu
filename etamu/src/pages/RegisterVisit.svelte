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
    .login-container{
      width: 400px;
      height: 300px;
      background: #edeff1;
      margin: 0px auto;
      padding-top: 20px;
      border-radius: 10px;
      -moz-border-radius: 10px;
      -webkit-border-radius: 10px;
    }

    input[type="text"]{
      display: block;
      width: 309px;
      height: 35px;
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
    }

    input[type="text"]:focus{
      border: 2px solid #1abc9d
    }
    
    button{
      display: block;
      background: #1abc9d;
      width: 314px;
      padding: 12px;
      cursor: pointer;
      color: #fff;
      border: 0px;
      margin: auto;
      border-radius: 5px;
      -moz-border-radius: 5px;
      -webkit-border-radius: 5px;
      font-size: 17px;
      transition: all 0.3s ease;
    }
    
    input[type="submit"]:hover{
      background: #09cca6
    }
</style>
