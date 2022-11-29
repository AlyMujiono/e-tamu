<script>
    import TopNav from "../components/TopNav.svelte";
    import axios from "axios";
    let visit_id = "";
    let state = null;
    let visit = undefined;
    async function searchVisit() {
        try {
            const response = await axios.get(
                `http://localhost:8000/api/v1/visits/${visit_id}`
            );
            visit = response.data.data;
            const responseGetStaff = await axios.get(
                `http://localhost:8000/api/v1/visit/users/${visit.user_visited_id}`
            );
            state = responseGetStaff.data.success;
            visit = {
                ...visit,
                user_visited_name: responseGetStaff.data.data.user_name,
            };
            console.log("visit : ", visit);
        } catch (error) {
            state = false;
            console.log("error : ", error);
        }
    }
</script>

<div class="container">
    {#if state == true}
        <TopNav title="ID Kunjungan : {visit.visit_id}" />
        <div class="status-container">
            <p class="status">Status : Disetujui.</p>
        </div>
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
                                style="color: white;"
                                src={"http://localhost:8000/" +
                                    visit.vaccine_certificate}
                                alt="sertifikat vaksin"
                            />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    {:else if state == false}
        <TopNav title="Cek Status Kunjungan" />
        <div class="form-container">
            <div class="input-container">
                <label class="visit-id" for="visit_id">Cek Kunjungan</label>
                <input
                    class="input-id"
                    type="text"
                    id="visit_id"
                    bind:value={visit_id}
                    placeholder="ID Kunjungan"
                />
            </div>
            <div>
                <div class="button-container">
                    <button on:click={searchVisit} disabled={!visit_id}
                        >Submit</button
                    >
                </div>
            </div>
            <div>
                <div class="btm-container">
                    <div class="btn-container">
                        <button
                            on:click={() => {
                                window.location.href = "";
                            }}
                            id="batal-btn">Kembali</button
                        >
                    </div>
                </div>
            </div>
            <h2>Id Kunjungan tidak ditemukan! Periksa kembali ID kunjungan</h2>
        </div>
    {:else}
        <TopNav title="Cek Status Kunjungan" />
        <div class="form-container">
            <div class="input-container">
                <label class="visit-id" for="visit_id">Cek Kunjungan</label>
                <input
                    class="input-id"
                    type="text"
                    id="visit_id"
                    bind:value={visit_id}
                    placeholder="ID Kunjungan"
                />
            </div>
            <div>
                <div class="button-container">
                    <button on:click={searchVisit} disabled={!visit_id}
                        >Submit</button
                    >
                </div>
            </div>
            <div>
                <div class="btm-container">
                    <div class="btn-container">
                        <button
                            on:click={() => {
                                window.location.href = backUri;
                            }}
                            id="batal-btn">Kembali</button
                        >
                    </div>
                </div>
            </div>
        </div>
    {/if}
</div>

<style>
    .status-container {
        position: absolute;
        width: 334.51px;
        height: 42.42px;
        right: 5%;
        top: 10px;

        background: #00b14c;
        border-radius: 5px;
    }
    .status {
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
    .btm-container {
        display: flex;
        flex-direction: row;
        justify-content: right;
        padding: 10px;
        gap: 10px;
    }
    .btn-container {
        display: flex;
        align-self: flex-end;
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
        position: absolute;
        left: 20%;
        top: 58%;
    }
    .top-container {
        display: flex;
        flex-direction: row;
        height: auto;
        align-self: center;
    }
    .field-container {
        background-color: #1a1a1a;
        padding: 2vh;
        margin: 2vh;
    }
    .left-container {
        display: flex;
        height: 100%;
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

    .button-container {
        display: flex;
        align-self: flex-end;
    }
    .form-container {
        position: absolute;
        width: 90%;
        height: 80%;
        left: 5%;
        right: 5%;
        top: 98px;

        background: #1a1a1a;
    }
    .visit-id {
        position: absolute;
        width: 60%;
        height: 56px;
        left: 30px;
        top: 30%;

        /* Heading-1 */
        font-style: normal;
        font-weight: 600;
        font-size: 48px;
        line-height: 56px;
        color: #ffffff;
    }
    .input-id {
        position: absolute;
        width: 60%;
        height: 37.97px;
        max-left: 281px;
        left: 20%;
        top: 45%;

        background: #37393a;
        border-radius: 5px;
    }
    input {
        color: #ffffff;
    }
    button {
        position: absolute;
        width: 261px;
        height: 40px;
        right: 20%;
        top: 58%;

        background: #406aa8;
        border-radius: 5px;

        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 0px;
        /* or 150% */

        color: #ffffff;
    }
    h2 {
        position: absolute;
        width: 60%;
        height: 30px;
        left: 20%;
        right: 20%;
        top: 65%;

        /* Text-1 */
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 30px;
        /* identical to box height, or 150% */

        /* Red */
        color: #f73c3c;
    }
    @media screen and (max-width: 500px) {
        .status {
            visibility: hidden;
        }
    }
</style>
