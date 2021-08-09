<script>
    import { Link } from "svelte-navigator";

    let user = {
        name: "",
        lastname: "",
        idno: "",
        birthDate: "",
        address: "",
        imageUrl: "",
        checked:false
    };

    function saveUser() {
        let users = localStorage.getItem("users");
        users=JSON.parse(users)
        if (!users ||users==undefined) {
            users = [];
        }
        console.log(users)
    
        users.push(user);
        localStorage.setItem("users", JSON.stringify(users));
    }
</script>

<main>
    <div class="column">
        <div class="row space-between align-center">
            <span class="text-1">Name:</span>
            <input type="text" class="text-box" bind:value={user.name} />
        </div>
        <div class="row space-between align-center">
            <span class="text-1">Family Name:</span>
            <input type="text" class="text-box" bind:value={user.lastname} />
        </div>
        <div class="row space-between align-center">
            <span class="text-1">ID No:</span>
            <input type="number" class="text-box" bind:value={user.idno} />
        </div>
        <div class="row space-between align-center">
            <span class="text-1">Birth date:</span>
            <input type="date" class="text-box" bind:value={user.birthDate} />
        </div>
        <div class="row space-between align-center">
            <span class="text-1"> Address:</span>
            <input type="text" class="text-box" bind:value={user.address} />
        </div>
        <div class="row">
            <span class="text-1">Profile Pic:</span>
            <div class="upload-card">
                <img src="/icon/camera.svg" alt="upload" />
            </div>
        </div>
        <div class="row justify-end">
            <Link to="/">
                <div class="btn denger" style="margin-right: 10px;">back</div>
            </Link>
            <Link to="/">
                <div class="btn" on:click={saveUser}>save</div>
            </Link>
        </div>
    </div>
</main>

<style scoped>
    main {
        margin: 35px 25px 0px 25px;
    }
   
    .text-1 {
        width: 150px;
    }
    .row {
        margin-top: 10px;
    }
    .justify-end {
        margin-top: 20px;
    }
    .upload-card {
        width: 100px;
        height: 120px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #ffffff;
        border: 1px solid #6eebe7;
        box-sizing: border-box;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.25);
        border-radius: 0px 0px 5px 5px;
    }
  
</style>
