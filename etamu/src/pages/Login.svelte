<script>
    import axios from "axios";
    import Cookies from "js-cookie";
    let userEmail = "";
    let userPassword = "";

    async function Login() {
        try {
            const response = await axios.post(
                "http://localhost:8000/api/v1/login",
                {
                    user_email: userEmail,
                    user_password: userPassword,
                }
            );
            const res = response.data;
            var expTime = new Date(new Date().getTime() + 60 * 60 * 1000);

            Cookies.set("token", res.data.token, {
                expires: expTime,
            });
        } catch (err) {
            console.log("Error : ", err);
        }
    }
</script>

<div class="main-container">
    <div class="container">
        <div class="cover">
            <img class="backImg" src="src\assets\img\33.jpg" alt="" />
        </div>
        <div class="forms">
            <div class="form-content">
                <div class="login-form">
                    <div class="title">Login</div>
                    <br />
                    <p>silahkan masukan info login anda</p>
                    <form action="">
                        <div class="input-boxes">
                            <div class="input-box">
                                <i class="fas fa-envelope" />
                                <label for="user_email" />
                                <input
                                    id="user_email"
                                    type="text"
                                    placeholder="Masukan email"
                                    required
                                    bind:value={userEmail}
                                />
                            </div>
                            <div class="input-box">
                                <i class="fas fa-lock" />
                                <label for="user_password" />
                                <input
                                    id="user_password"
                                    type="password"
                                    placeholder="Masukan password"
                                    required
                                    bind:value={userPassword}
                                />
                            </div>
                            <div class="button input-box">
                                <input type="submit" value="Login" />
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>

<style>
    /* Google Font Link */

    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Poppins", sans-serif;
    }

    :root {
		background: #828282;
	}
	
    .main-container {
        min-height: 85vh;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 30px;
    }

    .container {
        position: relative;
        max-width: 850px;
        width: 100%;
        background: #fff;
        padding: 40px 30px;
        box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
        perspective: 2700px;
    }

    .container .cover {
        position: absolute;
        top: 0;
        left: 25%;
        height: 100%;
        width: 50%;
        z-index: 98;
        transition: all 1s ease;
        transform-origin: left;
        transform-style: preserve-3d;
    }

    .container .cover img {
        position: absolute;
        height: 100%;
        width: 100%;
        object-fit: cover;
        z-index: 10;
    }

    .container .forms {
        height: 100%;
        width: 100%;
        background: #fff;
    }

    .container .form-content {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .forms .form-content .title {
        position: fixed;
        font-size: 24px;
        font-weight: 500;
        color: #333;
    }

    .forms .form-content .title:before {
        content: "";
        position: absolute;
        left: 0;
        bottom: 0;
        height: 3px;
        width: 25px;
        background: #7d2ae8;
    }

    .forms .form-content .input-boxes {
        margin-top: 30px;
    }

    .forms .form-content .input-box {
        display: flex;
        align-items: center;
        height: 50px;
        width: 100%;
        margin: 10px 0;
        position: relative;
    }

    .form-content .input-box input {
        height: 100%;
        width: 100%;
        outline: none;
        border: none;
        padding: 0 30px;
        font-size: 16px;
        font-weight: 500;
        border-bottom: 2px solid rgba(0, 0, 0, 0.2);
        transition: all 0.3s ease;
    }

    .form-content .input-box input:focus,
    .form-content .input-box input:valid {
        border-color: #7d2ae8;
    }

    .form-content .input-box i {
        position: absolute;
        color: #7d2ae8;
        font-size: 17px;
    }

    .forms .form-content .button {
        color: #fff;
        margin-top: 40px;
    }

    .forms .form-content .button input {
        color: #fff;
        background: #7d2ae8;
        border-radius: 6px;
        padding: 0;
        cursor: pointer;
        transition: all 0.4s ease;
    }

    .forms .form-content .button input:hover {
        background: #5b13b9;
    }

    .forms .form-content label {
        color: #5b13b9;
        cursor: pointer;
    }

    .forms .form-content label:hover {
        text-decoration: underline;
    }

    @media (max-width: 730px) {
        .container .cover {
            display: none;
        }
        .container #flip:checked ~ .forms .login-form {
            display: none;
        }
    }
</style>
