<script>
    import axios from "axios"; 
	import {getContext} from "svelte";
    export let deletedID = undefined;
    export let token = undefined;
	console.log(token);
	const { close } = getContext('simple-modal');
    async function deleteUserByID(id) {
		try {
			const response = await axios.delete(
				`https://api-e-tamu.herokuapp.com/api/v1/users/${id}`,
				{
					headers: {
						Authorization: `Bearer ${token}`,
					},
				}
			);

			return response.data.data;
		} catch (error) {
			return null;
		}
	}
</script>


<div>
	<p> <b> Hapus User? </b> </p>
	<p>Aksi ini tidak dapat diurungkan</p>
    <button id="delete" on:click|preventDefault={async () => {
		let deletedUser =
			await deleteUserByID(
				deletedID
			);
		console.log(deletedUser);
		window.location.href = '/admin/daftaruser';
	}}>Ya</button>
    <button id="close" on:click={close} >Tidak</button>
</div>

<style>
	div {
		display: flex;
		flex-flow: column;
		justify-content: center;
		align-items: center;
		height: 200px;
		margin : 0;
	}

	#delete {
		background-color: red;
		color: white;
	}
	#close {
		margin-top: 10px;
		margin-bottom: 2px;
		border: solid black 1px;
	}
</style>