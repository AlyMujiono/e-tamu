<script>
	import axios from "axios";
    import jsCookie from "js-cookie";

	export let selectedUser;
	export let backUri;
	console.log(selectedUser);

    let token = jsCookie.get("token");
    
</script>

<h1>Detail Kunjungan</h1>
<div class="content-field">
	<div class="form-field">
		<div class="left-container">
                    <div class="input-container">
                        <label class="input-label" for="nama-lengkap">Nama Lengkap</label>
                        <input type="text" name="nama-lengkap" id="nama-lengkap" class="input-field" value="{selectedUser.guest_name}"     
                        readonly>
                    </div>
                    <div class="input-container">
                        <label class="input-label" for="email">Email</label>
                        <input type="text" name="email" id="email" class="input-field" value="{selectedUser.guest_email}" readonly>
                    </div>
                    <div class="input-container">
                        <label class="input-label" for="tujaun">Tujuan</label>
                        <input type="text" name="tujuan" id="tujuan" class="input-field" value="{selectedUser.visit_intention}" readonly>
                    </div>
                    <div class="input-container">
                        <label class="input-label" for="jumlah-pengunjung">Jumlah Pengunjung</label>
                        <input type="number" name="jumlah pengunjung" id="jumlah-pengunjung" class="input-field" placeholder="{selectedUser.guest_count}" readonly>
                    </div>
                    <div class="input-container">
                        <label class="input-label" for="transportasi">Transportasi</label>
                        <input type="text" name="transportasi" id="transportasi" class="input-field" value="{selectedUser.transportation}"
                        readonly>
                    </div>
                    <div class="input-container">
                        <label class="input-label" for="tanggal">Tanggal Kunjungan</label>
                        <input type="text" name="tanggal" id="tanggal" class="input-field" value="{selectedUser.visit_date}" 
                        readonly>
                    </div>
                    <div class="input-container">
                        <label class="input-label" for="waktu">Waktu Kunjungan</label>
                        <input type="text" name="waktu" id="waktu" class="input-field" value="{selectedUser.visit_hour}" 
                        readonly>
                    </div>
                </div>
                <div class="middle-container">
                    <div class="input-container">
                        <label for="tertuju" class="input-label">Tertuju</label>
                        <input type="text" name="tertuju" id="tertuju" class="input-field" value="{selectedUser.user_visited_name}" 
                        readonly>
                    </div>
                </div>
                <div class="right-container">
                    <div class="input-container">
                        <label class="input-label" for="sertifikatVaksin">Sertifikat Vaksin</label>
                        <img style="color: white; height: 150px; width: 290px; background: #ffffff12;" src="{"https://api-e-tamu.herokuapp.com//"+selectedUser.vaccine_certificate}" alt="sertifikat vaksin">
                        
                    </div>
                    <div>
                        {#if selectedUser.confirmation === "1"}
                            {#if String(selectedUser.visit_status).toLowerCase() === "belum datang"}
                            <div class="status-red">
                                <label for="">Status : {selectedUser.visit_status}</label>
                            </div>
                            {:else if String(selectedUser.visit_status).toLowerCase() === "sedang berlangsung"}
                            <div class="status-blue">
                                <label for="">Status : {selectedUser.visit_status}</label>
                            </div>
                            {:else if String(selectedUser.visit_status).toLowerCase() === "selesai"}
                            <div class="status-green">
                                <label for="">Status : {selectedUser.visit_status}</label>
                            </div>
                            {/if}
                        {:else}
                            {#if selectedUser.confirmation === ""}
                            <div class="status-red">
                                <label for="">Status : Belum Dikonfirmasi</label>
                            </div>
                            {:else if selectedUser.confirmation === "0"}
                            <div class="status-red">
                                <label for="">Status : Ditolak</label>
                            </div>
                            {/if}
                        {/if}
                    </div>
                </div>  
    <div class="bottom-container">
	    <div class="button-container">
	        <button on:click={() => {window.location.href = backUri}} id="batal-btn"
	            >Kembali</button
	        >
	    </div>
	</div>
	</div>
	
</div>
<style>
h1 {
	color: white;
	font-size: 36px;
}
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: sans-serif;
}


/* .content {
	flex: 1 1 0;
	padding: 2rem;
}

.content h1 {
	width: 252px;
	height: 44px;
	left: 252px;
	top: 91px;
	
	font-style: normal;
	font-weight: 600;
	font-size: 30px;
	line-height: 44px;

	
	color: #FFFFFF;
}

.content p {
	color: #707793;
} */

.content-field {
	width: 100%;
	height: 520px;
	margin-top: 10px;
	padding: 10px;	
	
	background: #37393A;
}
.form-field {	
	display: flex;
	flex-direction: row;
}
.bottom-container {
    display: flex;
    flex-direction: row;
    justify-content: right;
    padding: 10px;
    gap: 10px;
}
.left-container {
    display: flex;
    height: 100%;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    /* padding-top: 3vh; */
}
.right-container {
    display: flex;
    height: auto;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    /* padding-top: 3vh; */
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
.input-field {
    padding: 1.5vh;
    border-radius: 1vh;
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
    /* align-items: flex-start; */
    /* justify-content: flex-start; */
}
.middle-container label {
    display: flex;
    align-self: flex-start;
}

.button-container {
    display: flex;
    align-self: flex-end;
    
}
#batal-btn {
	width: 200px;
	height: 36.9px;
	
	background: #F73C3C;
	border-radius: 5px;
	font-style: normal;
	font-weight: 400;
	font-size: 20px;
	line-height: 30px;
	/* or 150% */
	
	color: #FFFFFF;
}
#konfirmasi-btn {
	width: 200px;
	height: 36.9px;
	
	background: #406AA8;
	border-radius: 5px;
	font-style: normal;
	font-weight: 400;
	font-size: 20px;
	line-height: 30px;
	/* or 150% */
	
	color: #FFFFFF;
}

.status-green {
        width: auto;
        height: 36.9px;

        background: #00b14c;
        border-radius: 5px;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 30px;
        padding: 0 10px;
        margin: 10px;
        /* or 150% */

        color: #ffffff;
    }

    .status-red {
        width: auto;
        height: 36.9px;

        background: red;
        border-radius: 5px;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 30px;
        padding: 0 10px;
        margin: 10px;
        /* or 150% */

        color: #ffffff;
    }
    .status-blue {
        width: auto;
        height: 36.9px;

        background: blue;
        border-radius: 5px;
        font-style: normal;
        font-weight: 400;
        font-size: 20px;
        line-height: 30px;
        padding: 0 10px;
        margin: 10px;
        /* or 150% */

        color: #ffffff;
    }

/* @media (max-width: 1024px) {
	.sidebar {
		max-width: 200px;
	}
}

@media (max-width: 768px) {
	.menu-toggle {
		display: block;
	}
	.content {
		padding-top: 8rem;
	}
	.sidebar {
		position: fixed;
		top: 0;
		left: -300px;
		height: 100vh;
		width: 100%;
		max-width: 300px;
		transition: 0.2s linear;
	}

	.open {
		left: 0;
	}
	.logout-header {
		visibility: hidden;
	}
	.logout-sidebar {
		visibility: visible;
	}
} */
</style>