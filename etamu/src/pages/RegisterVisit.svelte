<script>
    import axios from 'axios';
    import Cookies from 'js-cookie';
    import Select from 'svelte-select';
    let fullName = '';
    let email = '';
    let visitIntention ='';
    let visitDate = '';
    let visitHour = '';
    let guestCount = undefined;
    let transportation = '';
    let token = Cookies.get("token");
    let visitedStaffID = undefined;
    let vaccineCertificate = undefined;
    const optionIdentifier = 'id';
    const labelIdentifier = 'user_name';

    async function getAllUsers(text = '') {
        try {
            const response = await axios.get(`http://localhost:8000/api/v1/visit/users?name=${text}`)
            console.log("Response : ", response.data.data)
            return response.data.data;
        } catch (error) {
            console.log("Error : ", error)
            return [];
        }
    }

    function handleSelect(event) {
        visitedStaffID = event.detail.user_id;
    }
    function handleClear() {
        visitedStaffID = undefined;
    }
    async function submitVisit() {
        let file = undefined;

        if (vaccineCertificate && vaccineCertificate[0]) {
            file = vaccineCertificate[0];
        }
        console.log({
            fullName,
            email,
            visitIntention,
            visitDate,
            visitHour,
            guestCount,
            transportation,
            token,
            visitedStaffID,
            file
        })

        let bodyFormData = new FormData();
        bodyFormData.append('guest_name', fullName);
        bodyFormData.append('guest_email', email);
        bodyFormData.append('user_visited_id', visitedStaffID);
        bodyFormData.append('visit_intention', visitIntention);
        bodyFormData.append('visit_status', 'belum datang');
        bodyFormData.append('guest_count', guestCount);
        bodyFormData.append('visit_date', visitDate);
        bodyFormData.append('visit_hour', visitHour);
        bodyFormData.append('transportation', transportation);
        bodyFormData.append('vaccine_certificate', file);

        const response = await axios({
            method: 'post',
            url: 'http://localhost:8000/api/v1/visit/create',
            data : bodyFormData,
            headers: { "Content-Type": "multipart/form-data" },
        })

        console.log("Response : ", response.data.data)
        var expTime = new Date(new Date().getTime() + 60 * 60 * 1000);

        Cookies.set("otp", response.data.data.otp_token, {
            expires: expTime
        })
        window.location.href = "/registerVisit/verify";
    }
</script>

<div class="main-container">
    <div class="form-container">
        <div class="input-container">
            <label for="fullname">Nama Lengkap</label>
            <input type="text" id="fullname" bind:value={fullName}>
        </div>
        <div class="input-container">
            <label for="email">Email</label>
            <input type="text" id="email" bind:value={email}>
        </div>
        <div class="input-container">
            <label for="visit_intention">Maksut Kunjungan</label>
            <input type="text" id="visit_intention" bind:value={visitIntention}>
        </div>
        <div class="input-container">
            <label for="visit_date">Tanggal Kunjungan</label>
            <input type="date" id="visit_date" bind:value={visitDate}>
        </div>
        <div class="input-container">
            <label for="visit_hour">Jam Kunjungan</label>
            <input type="time" id="visit_hour" min="09:00" max="17:00" bind:value={visitHour}>
        </div>
        <div class="input-container">
            <label for="guest_count">Jumlah Orang</label>
            <input type="number" id="guest_count" bind:value={guestCount} min=0>
        </div>
        <div class="input-container">
            <label for="transportation">Transportasi</label>
            <input type="text" id="transportation" bind:value={transportation} >
        </div>
        <div class="input-container">
            <label for="staffVisited">Staff</label>
            <Select id="staffVisited" {optionIdentifier} {labelIdentifier} loadOptions={getAllUsers} on:select={handleSelect} on:clear={handleClear}></Select>
        </div>
        <div class="input-container">
            <label for="vaccineCertificate">Sertifikat Vaksin</label>
            <input type="file" id="vaccineCertificate" accept="image/png, image/jpeg" bind:files={vaccineCertificate}>
        </div>
        <div class="button-container">
            <button on:click={submitVisit} disabled={!fullName || !email || !visitIntention || !visitDate || !visitHour || !guestCount || !transportation || !visitedStaffID}>Submit</button>
        </div>

    </div>
</div>

<style>
    .input-container {
        display: flex;
        flex-direction: column;
        gap: 5px;
        margin-bottom: 0.2em;
    }
</style>