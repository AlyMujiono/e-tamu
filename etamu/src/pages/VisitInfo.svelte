
<script>
    
    import axios from 'axios';
    let visit_id = '';
    let state = null;
    let visit = undefined;
    async function searchVisit () {
        try {
            const response = await axios.get(`http://localhost:8000/api/v1/visits/${visit_id}`);
            visit = response.data.data;
            const responseGetStaff = await axios.get(`http://localhost:8000/api/v1/visit/users/${visit.user_visited_id}`)
            state = responseGetStaff.data.success;
            visit = {...visit, user_visited_name : responseGetStaff.data.data.user_name};
            console.log("visit : ", visit);

        } catch (error) {
            state = false;
            console.log("error : ", error);
        }

    }
</script>

<div class="container">
    {#if state == true}
    <div class="field-container">
        <div class="value-container">
            <p>ID Kunjungan : {visit.visit_id}</p>
            <p>Nama Pengunjung : {visit.guest_name}</p>
            <p>Email Pengunjung : {visit.guest_email}</p>
            <p>Maksut Kunjungan : {visit.visit_intention}</p>
            <p>Tanggal Kunjungan : {visit.visit_date}</p>
            <p>Waktu Kunjungan : {visit.visit_hour}</p>
            <p>Jumlah Pengunjung : {visit.guest_count}</p>
            <p>Transportasi : {visit.transportation}</p>
            <img src="{visit.vaccine_certificate}" alt="sertifikat vaksin">
        </div>
    </div>
    {:else if state == false}
    <h2>Kunjungan Tidak ditemukan</h2>
    {:else}
    <div class="form-container">
        <div class="input-container">
            <label for="visit_id">ID Kunjungan</label>
            <input type="text" id="visit_id" bind:value={visit_id}>
        </div>
        <div class="button-container">
            <button on:click={searchVisit} disabled={!visit_id}>Submit</button>
        </div>
    </div>
    {/if}
    
</div>