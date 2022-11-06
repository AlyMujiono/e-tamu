<script>
    import axios from 'axios'
    const { each } = require("svelte/internal");
    let visits = []
    let response = axios.get("")
</script>
<div class="container">
    <div class="side-bar-container">
        <button class="side-bar-button">Daftar User</button>
        <button class="side-bar-button">List Kunjungan</button>
    </div>
    <div class="content-container">
        <div class="top-bar-container">

        </div>
        <div class="middle-bar-container">

        </div>
        <div class="list-container">
            <table>
                <tr>
                    <th>Nama Lengkap</th>
                    <th>Roles</th>
                    <th>Aksi</th>
                </tr>
                
            </table>
        </div>
    </div>
</div>