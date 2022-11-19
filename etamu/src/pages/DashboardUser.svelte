<script>
	import axios from "axios";
	import Cookie from "js-cookie";
	import { onMount } from "svelte";
	import TopNav from "../components/TopNav.svelte";
	import DetailKunjungan from "../components/DetailKunjungan.svelte";
	let navOpen = false;
	let listOfVisit = [];
	let startDate;
	let endDate;
	let token = Cookie.get('token');
	let selectedID;
	let state;
	
	function handleNav() {
		navOpen = !navOpen;		
	}
	async function getVisitByID(id) {
		try {
			const response = await axios.get(
						`http://localhost:8000/api/v1/visits/${id}`, 
						{
							headers: {
								"Authorization": `Bearer ${token}`
							}
						}
					);
			
					return response.data.data;
		} catch (error) {
			return null;
		}
	}
	async function getAllVisit() {
		try {
				const response = await axios.get(
					`http://localhost:8000/api/v1/visits`, 
					{
						headers: {
							"Authorization": `Bearer ${token}`
						}
					}
				);
				listOfVisit = response.data.data;
				
				listOfVisit.forEach(async (visit, index) => {
					const res = await axios.get(
						`http://localhost:8000/api/v1/visit/users/${visit.user_visited_id}`
					)

					let user_visited_name = res.data.data.user_name;
					listOfVisit[index] = {...visit, user_visited_name};
				});
				console.log(listOfVisit);
				listOfVisit = listOfVisit
			} catch (error) {
				listOfVisit = [];
			}
	}

	async function getAllVisitByDate() {
		if (!startDate || !endDate) {
			getAllVisit();
			return
		}
		
		try {
				const response = await axios.get(
					`http://localhost:8000/api/v1/visits/date`, 
					{
						headers: {
							"Authorization": `Bearer ${token}`
						}, 
						params: { start_date: startDate, end_date: endDate }
					}
				);
				listOfVisit = response.data.data;
				
				listOfVisit.forEach(async (visit, index) => {
					const res = await axios.get(
						`http://localhost:8000/api/v1/visit/users/${visit.user_visited_id}`
					)

					let user_visited_name = res.data.data.user_name;
					listOfVisit[index] = {...visit, user_visited_name};
				});
				console.log(listOfVisit);
				listOfVisit = listOfVisit
			} catch (error) {
				listOfVisit = [];
			}
	}

	onMount(
		async () => {

			/* if (token === '') {
				window.location.href = "/login";
			} */

			try {
				const response = await axios.get(
					`http://localhost:8000/api/v1/visits`, 
					{
						headers: {
							"Authorization": `Bearer ${token}`
						}
					}
				);
				listOfVisit = response.data.data;
				
				listOfVisit.forEach(async (visit, index) => {
					const res = await axios.get(
						`http://localhost:8000/api/v1/visit/users/${visit.user_visited_id}`
					)

					let user_visited_name = res.data.data.user_name;
					listOfVisit[index] = {...visit, user_visited_name};
				});
				listOfVisit = listOfVisit
			} catch (error) {
				if (error.response.status === 401) {
					window.location.href = "/login";
				}
				listOfVisit = [];
			}
			
			
		}
	)

</script>

<TopNav/>
<button class="logout-header">Logout</button>
<div class="app">
		<div class="menu-toggle" class:change={navOpen} on:click={handleNav}>
			<div class="hamburger">
				<span></span>
			</div>
		</div>

		<aside class="sidebar" class:open={navOpen}>
			<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Svelte_Logo.svg/1200px-Svelte_Logo.svg.png" class="profile">
			<h3>User</h3>			

			<button class="logout-sidebar">Logout</button>

		</aside>

		<main class="content">
			{#if state === 'detail'}
			<DetailKunjungan selectedID={selectedID} />
			
			{:else}
			<h1>Daftar Kunjungan</h1>
			<div class="spasi">
				<div class="row">
					<div class="input-container">
            		    <label class="input-label" for="tanggal">Tanggal Awal</label>
            		    <input on:change={getAllVisitByDate} type="date" name="tanggal" id="tanggal" class="input-field" placeholder="Tanggal 	Kunjungan" bind:value={startDate} >
            		</div>
            		<div class="input-container">
            		    <label class="input-label" for="tanggal">Tanggal Akhir</label>
            		    <input on:change={getAllVisitByDate} type="date" name="tanggal" id="tanggal" class="input-field" placeholder="Tanggal 	Kunjungan" bind:value={endDate} >
            		</div>
            	</div>
            </div>
            <div id="scrollingBlock">
            	<table>
            		<thead>
						<tr>
							<th>Nama Tamu</th>
							<th>Yang dituju</th>
							<th>Waktu</th>
							<th style="display: flex; justify-content: center; border: 0px;">Aksi</th>
						<tr/>
					</thead>
					<tbody>
						{#each listOfVisit as visit}
							<tr>
								<td>{visit.guest_name}</td>
								<td>{visit.user_visited_name}</td>
								<td>{visit.visit_date}</td>
								<td>
									<div class="row-button">
										<button on:click|preventDefault={async () => {
											selectedID = await getVisitByID(visit.visited_id);/*masih ngaco*/
											state = 'detail';
										}} class="btn-biru">Detail</button>
									</div>
								</td>
							</tr>
						{/each}
					</tbody>
            	</table>
            </div>
            {/if}
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
	color: white;
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
	width: 304px;
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
.spasi {
	display: flex;
    flex-direction: row;
    justify-content: right;
}
.btn-expdata {
	width: 107px;
	height: 40px;
	
	/* Blue */
	background: #406AA8;
	border-radius: 4px;
	font-style: normal;
	font-weight: 400;
	font-size: 16px;
	line-height: 24px;
	/* identical to box height, or 150% */
	
	/* White */
	color: #FFFFFF;
}
.row {
	display: flex;
    flex-direction: row;
    gap: 5px;
    margin-bottom: 0.2em;
    justify-content: right;
}
.input-container {
    display: flex;
    flex-direction: column;
    gap: 5px;
    margin-bottom: 0.2em;
}
input[type="date"] {
    display: block;
    width: 120px;
    height: 25px;
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

input[type="date"]:focus {
    border: 2px solid #1abc9d;
}

#scrollingBlock {
	height: 440px;
	border: 2px solid black;
	/*box-shadow: 10px 5px 5px red;*/
	overflow-y: scroll;
}

table {
	border: 1px solid #37393A;
	background-color: #37393A;;
	width: 100%;
	text-align: left;
	border-collapse: collapse;
}
table td, table th {
	border: 1px solid #37393A;
	padding: 10px 10px;
	color: white;
}
table tbody td {
	font-size: 13px;
}	
table tr:nth-child(even) {
	background: #37393A;
}
table thead {
	background: #37393A;
	border-bottom: 2px solid #444444;	
    position: sticky;
    position: -webkit-sticky;
    top: 0;
    z-index: 999;
}
table thead th {
	font-size: 15px;
	font-weight: bold;
	color: #FFFFFF;
	border-bottom: 2px solid #D0E4F5;
}
table thead th:first-child {
	border-left: none;
}

.row-button {
	display: flex;
    flex-direction: row;
    gap: 5px;
    margin-bottom: 0.2em;
    justify-content: center;
}
.btn-biru {
	width: 50px;
	height: 25px;
	
	/* Blue */	
	background: #406AA8;
	border-radius: 4px;
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