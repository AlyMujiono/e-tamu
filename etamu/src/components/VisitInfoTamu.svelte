<script>
    import TopNav from "../components/TopNav.svelte";
    export let visit = undefined;
</script>

<div class="container">
        <TopNav title="ID Kunjungan : {visit.visit_id}" />
            {#if visit.confirmation === "1"}
                    {#if String(visit.visit_status).toLowerCase() === "belum datang"}
                    <div class="status-container-red">
                        <div class="status">
                            <label for="">Status : {visit.visit_status}</label>
                        </div>
                    </div>
                    {:else if String(visit.visit_status).toLowerCase() === "sedang berlangsung"}
                    <div class="status-container-blue">
                        <div class="status">
                            <label for="">Status : {visit.visit_status}</label>
                        </div>
                    </div>
                    {:else if String(visit.visit_status).toLowerCase() === "selesai"}
                    <div class="status-container-green">
                        <div class="status">
                            <label for="">Status : {visit.visit_status}</label>
                        </div>
                    </div>
                    {/if}
                
                {:else}
                    {#if visit.confirmation === ""}
                    <div class="status-container-red">
                        <div class="status">
                            <label for="">Status : Belum Dikonfirmasi</label>
                        </div>
                    </div>
                    {:else if visit.confirmation === "0"}
                    <div class="status-container-red">
                        <div class="status">
                            <label for="">Status : Ditolak</label>
                        </div>
                    </div>
                    {/if}
                {/if}
        <div class="main-container">
            <div class="field-container">
                <div class="top-container">
                    <div class="left-container">
                        <div class="input-container">
                            <label class="input-label" for="nama-lengkap"
                                >Nama Lengkap</label
                            >
                            <input
                                type="text"
                                name="nama-lengkap"
                                id="nama-lengkap"
                                class="input-field"
                                value={visit.guest_name}
                                readonly
                            />
                        </div>
                        <div class="input-container">
                            <label class="input-label" for="email">Email</label>
                            <input
                                type="text"
                                name="email"
                                id="email"
                                class="input-field"
                                value={visit.guest_email}
                                readonly
                            />
                        </div>
                        <div class="input-container">
                            <label class="input-label" for="tujaun"
                                >Tujuan</label
                            >
                            <input
                                type="text"
                                name="tujuan"
                                id="tujuan"
                                class="input-field"
                                value={visit.visit_intention}
                                readonly
                            />
                        </div>
                        <div class="input-container">
                            <label class="input-label" for="jumlah-pengunjung"
                                >Jumlah Pengunjung</label
                            >
                            <input
                                type="number"
                                name="jumlah pengunjung"
                                id="jumlah-pengunjung"
                                class="input-field"
                                placeholder={visit.guest_count}
                                readonly
                            />
                        </div>
                        <div class="input-container">
                            <label class="input-label" for="transportasi"
                                >Transportasi</label
                            >
                            <input
                                type="text"
                                name="transportasi"
                                id="transportasi"
                                class="input-field"
                                value={visit.transportation}
                                readonly
                            />
                        </div>
                        <div class="input-container">
                            <label class="input-label" for="tanggal"
                                >Tanggal Kunjungan</label
                            >
                            <input
                                type="text"
                                name="tanggal"
                                id="tanggal"
                                class="input-field"
                                value={visit.visit_date}
                                readonly
                            />
                        </div>
                        <div class="input-container">
                            <label class="input-label" for="waktu"
                                >Waktu Kunjungan</label
                            >
                            <input
                                type="text"
                                name="waktu"
                                id="waktu"
                                class="input-field"
                                value={visit.visit_hour}
                                readonly
                            />
                        </div>
                        <div class="bottom-container">
                            <div class="button-container">
                                <button
                                    on:click={() => {
                                        window.location.href = "/visitinfo";
                                    }}
                                    id="batal-btn">Kembali</button
                                >
                            </div>
                        </div>
                    </div>
                    <div class="middle-container">
                        <div class="input-container">
                            <label for="tertuju" class="input-label"
                                >Tertuju</label
                            >
                            <input
                                type="text"
                                name="tertuju"
                                id="tertuju"
                                class="input-field"
                                value={visit.user_visited_name}
                                readonly
                            />
                        </div>
                    </div>
                    <div class="right-container">
                        <div class="input-container">
                            <label class="input-label" for="sertifikatVaksin"
                                >Sertifikat Vaksin</label
                            >
                            <img
                                style="color: white;height: 150px; width: 290px; background: #ffffff12;"
                                src={"http://localhost:8000/" +
                                    visit.vaccine_certificate}
                                alt="sertifikat vaksin"
                            />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

<style>
    .status-container-green {
        position: absolute;
        width: 334.51px;
        height: 42.42px;
        right: 5%;
        top: 10px;

        background: #00b14c;
        border-radius: 5px;
    }
    .status-container-blue {
        position: absolute;
        width: 334.51px;
        height: 42.42px;
        right: 5%;
        top: 10px;

        background: blue;
        border-radius: 5px;
    }
    .status-container-red {
        position: absolute;
        width: 334.51px;
        height: 42.42px;
        right: 5%;
        top: 10px;

        background: red;
        border-radius: 5px;
    }
    .status{
        margin: 5px;

        /* Heading-4 */
        font-style: normal;
        font-weight: 600;
        font-size: 20px;
        line-height: 28px;

        /* or 140% */
        align-items: center;
        text-align: center;

        color: #ffffff;
    }
    .main-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        height: 100vh;
        align-self: center;
        /* justify-content: space-between; */
        width: auto;
    }
    #batal-btn {
        width: 200px;
        height: 36.9px;
        background: #f73c3c;
        border-radius: 5px;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        color: #ffffff;
        /* position: absolute; */
        /* left: 20%; */
        /* top: 58%; */
    }
    .top-container {
        display: flex;
        flex-direction: row;
        height: auto;
        align-self: center;
        background-color: #1a1a1a;
    }
    .field-container {
        background-color: #1a1a1a;
        padding: 2vh;
        margin: 2vh;
        height: auto;
    }
    .left-container {
        display: flex;
        height: auto;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
    }
    .right-container {
        display: flex;
        height: auto;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
    }
    .right-container label {
        display: flex;
        align-self: flex-start;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        margin: 0.5vh 1vh;
    }
    .input-field {
        padding: 1.5vh;
        border-radius: 1vh;
        color: black;
    }
    .input-label {
        margin-bottom: 0.2vh;
        color: white;
        align-self: flex-start;
        font-size: small;
    }
    .middle-container {
        width: 50vh;
        display: flex;
        height: auto;
        flex-direction: column;
    }
    .middle-container label {
        display: flex;
        align-self: flex-start;
    }
    .bottom-container {
        display: flex;
        flex-direction: row;
        justify-content: right;
        align-self: center;
        padding: 10px;
        gap: 10px;
        /* margin-bottom: 1px; */
    }
    .button-container {
        display: flex;
        align-self: flex-end;
    }
  
    input {
        color: #ffffff;
    }
    button {
        /* position: absolute; */
        width: 261px;
        height: 40px;
        /* right: 20%;
        top: 58%; */

        background: #406aa8;
        border-radius: 5px;

        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 0px;
        /* or 150% */

        color: #ffffff;
    }
    @media screen and (max-width: 500px) {
        .status {
            visibility: hidden;
        }
    }
</style>
