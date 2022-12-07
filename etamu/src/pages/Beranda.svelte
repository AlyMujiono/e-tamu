<script>
    import Select from "svelte-select";
    import TopNav from "../components/TopNav.svelte";
    import GambarBeranda from "../assets/img/gambar-halaman-utama.jpeg";
    let navOpen = false;

    function handleNav() {
        navOpen = !navOpen;
    }
    const items = ["Staff", "Admin", "Security"];
</script>

<TopNav />
<button on:click={() => {
                                window.location.href = "/login";
                            }}
                            class="login-header">Login</button>

<div class="app">
    <main class="content">
        <div class="content-field">
            <div class="form-field">
                <div class="left-container">
                    <div class="input-container">
                        <label for=""
                            >Selamat Datang di <br />E-Tamu Labinta</label
                        >
                    </div>
                    <div class="input-container">
                        <p>
                            Silahkan Klik tombol ajukan untuk membuat permintaan
                            kunjungan. Jika ingin melihat status dan detail
                            kunjungan klik tombol cek status
                        </p>
                    </div>
                    <div class="btm-container">
                        <div class="bottom-container">
                            <div class="button-container">
                                <button on:click={() => {
                                window.location.href = "/registervisit";
                                }} id="visit-btn"
                                    >Ajukan</button
                                >
                            </div>
                        </div>
                        <div class="bottom-container">
                            <div class="button-container">
                                <button on:click={() => {
                                window.location.href = "/visitinfo";
                                }} id="end-btn"
                                    >Cek Status</button
                                >
                            </div>
                        </div>
                    </div>
                </div>
                <div class="right-container">
                    <!-- <div class="img"> -->
                        <img class="img" src="{GambarBeranda}" alt="Gambar Pabrik" />
                    <!-- </div> -->
                </div>
            </div>
        </div>
    </main>
</div>

<style>
    /* img {
        height: auto;
        width: auto;
    } */
    label {
        width: 462px;
        height: 112px;

        /* Heading-1 */

        font-style: normal;
        font-weight: 600;
        font-size: 48px;
        line-height: 56px;
        /* or 117% */

        /* White */

        color: #ffffff;
        /* Inside auto layout */

        flex: none;
        order: 0;
        align-self: stretch;
        flex-grow: 0;
    }
    p {
        color: white;
    }
    .img {
        position: absolute;
        width: 45%;
        height: 460px;
        left: 50%;
        top: 149px;
        background: #e0e0e0;
        border-radius: 8px;
    }
    .app {
        display: flex;
        min-height: 90vh;
    }
    .content {
        flex: 1 1 0;
        padding: 2rem;
    }
    .content-field {
        width: 100%;
        height: 517px;
        margin-top: 20px;
        padding: 10px;

        background: #37393a;
    }
    .form-field {
        display: flex;
        flex-direction: row;
    }
    .left-container {
        display: flex;
        width: 50%;
        height: 100%;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        /* padding-top: 3vh; */
        margin-top: 80px;
        text-align: left;
    }
    .right-container {
        width: 50%;
        display: flex;
        height: auto;
        flex-direction: column;
        /* align-items: flex-start; */
        /* justify-content: flex-start; */
    }
    .btm-container {
        display: flex;
        flex-direction: row;
        margin-bottom: 0px;
        margin-top: auto;
    }
    .bottom-container {
        display: flex;
        flex-direction: row;
        justify-content: right;
        padding: 10px;
        gap: 10px;
    }
    .button-container {
        display: flex;
        align-self: flex-end;
    }
    #visit-btn {
        width: 200px;
        height: 36.9px;

        background: #5f92de;
        border-radius: 5px;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 30px;
        /* or 150% */

        color: #ffffff;
    }
    #end-btn {
        width: 200px;
        height: 36.9px;

        background: #5f92de;
        border-radius: 5px;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 30px;
        /* or 150% */

        color: #ffffff;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        margin: 0.5vh 1vh;
        width: 90%;
        /* color : */
        /* --margin : 0 10vh; */
        /* --indicatorWidth : 100%; */
    }

    .login-header {
        position: absolute;
        right: 5%;
        top: 20px;

        width: 85px;
        height: 40px;

        /* Blue */
        background: #406aa8;
        border-radius: 4px;
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 24px;

        /* White */
        color: #ffffff;
    }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: sans-serif;
    }

    @media (max-width: 768px) {
        .img {
            left: 12%;
            width: 75%;
            height: 40%;
        }
        .left-container {
            left: 12%;
            margin-top: auto;
            margin-bottom: 20px;
            width: 100%;
            height: 100px;
        }
        .right-container {
            left: 12%;
            margin-top: 100%;
            margin-bottom: auto;
            width: 100%;
        }
        .form-field {
            flex-direction: column-reverse;
        }
    }
</style>
