<script>
	import Select from 'svelte-select';
  import TopNav from "../components/TopNav.svelte";
  import Cookie from 'js-cookie';
	let navOpen = false;
	
	function handleNav() {
		navOpen = !navOpen;		
	}
	const items = ['Staff', 'Admin', 'Security'];
</script>

<TopNav/>
<button on:click={()=>{
	Cookie.remove("token");
	window.location.href = "/login";
	}} class="logout-header">Logout</button>
<div class="app">
		<div class="menu-toggle" class:change={navOpen} on:click={handleNav}>
			<div class="hamburger">
				<span></span>
			</div>
		</div>

		<aside class="sidebar" class:open={navOpen}>
			<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Svelte_Logo.svg/1200px-Svelte_Logo.svg.png" class="profile">
			<h3>Admin</h3>
			
			<nav class="menu">
				<a href="/admin/daftarkunjungan" class="menu-item">Daftar Kunjungan</a>
				<a href="/admin/daftaruser" class="menu-item is-active">Daftar User</a>
			</nav>

			<button on:click={()=>{
				Cookie.remove("token");
				window.location.href = "/login";
				}} class="logout-sidebar">Logout</button>

		</aside>

		<main class="content">
			<h1>Buat/Edit User</h1>
			<div class="content-field">
				<div class="form-field">
					<div class="left-container">
            		    <div class="input-container">
            		        <label class="input-label" for="nama-lengkap">Nama Lengkap</label>
            		        <input type="text" name="nama-lengkap" id="nama-lengkap" class="input-field" placeholder="Nama Lengkap" 	>
            		    </div>
            		    <div class="input-container">
            		        <label class="input-label" for="email">Email</label>
            		        <input type="text" name="email" id="email" class="input-field" placeholder="Email" >
            		    </div>          	    
            		</div>
            		<div class="middle-container">
                		<div class="input-container">
            		        <label class="input-label" for="role">Jabatan / Role</label>
            		        <Select {items}></Select>
            		    </div>
            		    <div class="input-container">
            		        <label class="input-label" for="pswd">Password</label>
            		        <input type="text" name="pswd" id="pswd" class="input-field" placeholder="Password" >
            		    </div>    
                	</div>                	
        		</div>
        		<div class="bottom-container">
        		    <div class="button-container">
        		        <button on:click={() => {window.location.href = "/admin/daftaruser"}} id="batal-btn"
        		            >Batalkan</button
        		        >
        		    </div>
        		    <div class="button-container">
        		        <button id="konfirmasi-btn"
        		            >Konfirmasi</button
        		        >
        		    </div>
        		</div>
            </div>			
		</main>
	</div>

<style>
.logout-header {
    position: absolute;
    right: 5%;
    top: 20px;
    
    width: 85px;
	height: 40px;
	
	/* Blue */	
	background: #406AA8;
	border-radius: 4px;
	font-style: normal;
	font-weight: 400;
	font-size: 16px;
	line-height: 24px;	
	
	/* White */	
	color: #FFFFFF;
 }

* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: sans-serif;
}

.app {
	display: flex;
	min-height: 90vh;
}

.menu-toggle {
	display: none;
	position: fixed;
	top: 2rem;
	right: 2rem;
	width: 60px;
	height: 60px;
	border-radius: 99px;
	background-color: #2e3047;
	cursor: pointer;
}

.hamburger {
	position: relative;
	top: calc(50% - 2px);
	left: 50%;
	transform: translate(-50%, -50%);
	width: 32px;
}

.hamburger > span,
.hamburger > span::before,
.hamburger > span::after {
  display: block;
  position: absolute;
  width: 100%;
  height: 4px;
  border-radius: 99px;
  background-color: #FFF;
  transition-duration: .25s;
}

.hamburger > span::before {
  content: '';
  top: -8px;
}
.hamburger > span::after {
  content: '';
  top: 8px;
}
.menu-toggle.is-active .hamburger > span {
  transform: rotate(45deg);
}
.menu-toggle.is-active .hamburger > span::before {
  top: 0;
  transform: rotate(0deg);
}
.menu-toggle.is-active .hamburger > span::after {
  top: 0;
  transform: rotate(90deg);
}
.profile {
	width: 100px;
	height: 100px;
	margin-top: 20px;
	margin-bottom: 20px;
	border-radius: 50px;
}
.sidebar {
	flex: 1 1 0;
	max-width: 230px;
	padding: 2rem 1rem;
	background-color: #1A1A1A;;
}

.sidebar h3 {
	font-style: normal;
	font-weight: 600;
	font-size: 24px;
	line-height: 32px;
	/* identical to box height, or 133% */
	
	text-align: center;
}

.sidebar .menu {
	margin: 0 -1rem;
}

.sidebar .menu .menu-item {
	display: block;
	padding: 1em;
	color: #FFF;
	text-decoration: none;
	transition: 0.2s linear;
}

.sidebar .menu .menu-item:hover,
.sidebar .menu .menu-item.is-active {
	background: #406AA8;
	border-radius: 4px;
}

.sidebar .menu .menu-item:hover {
	background: #406AA8;
	border-radius: 4px;
}

.logout-sidebar { 
    width: 85px;
	height: 40px;
	
	/* Blue */	
	background: #406AA8;
	border-radius: 4px;
	font-style: normal;
	font-weight: 400;
	font-size: 16px;
	line-height: 24px;	
	
	/* White */	
	color: #FFFFFF;

	visibility: hidden;
 }

.content {
	flex: 1 1 0;
	padding: 2rem;
}

.content h1 {
	width: 252px;
	height: 44px;
	left: 252px;
	top: 91px;
	
	/* Heading-2 */
	font-style: normal;
	font-weight: 600;
	font-size: 36px;
	line-height: 44px;

	/* White */
	color: #FFFFFF;
}

.content p {
	color: #707793;
}

.content-field {
	width: 100%;
	height: 517px;
	margin-top: 20px;
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
    margin-top: 150px;
    padding: 10px;
    gap: 10px;
}
.left-container {
    display: flex;
    width: 50vh;
    height: 100%;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    /* padding-top: 3vh; */
}
.right-container {
    display: flex;
    height: 100%;
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
@media (max-width: 1024px) {
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
}
</style>