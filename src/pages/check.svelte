<script>
    import { onMount } from "svelte";
    import { useNavigate } from "svelte-navigator";
    const navigate = useNavigate();

    import { Link } from "svelte-navigator";
    import { user, indexUser } from "../stores";
    let userData = {};
    let editing = {
        name: false,
        lastname: false,
        idno: false,
        birthDate: false,
    };
    function editable(key, value) {
        editing[key] = value;
    }
    onMount(() => {
        userData = $user;
        console.log(userData);
        if (!userData || userData == undefined) {
            navigate("/", { replace: true });
        }
    });
    function editUser() {
        let users = JSON.parse(localStorage.getItem("users"));
        users[$indexUser] = userData;
        localStorage.setItem("users", JSON.stringify(users));
        navigate("/", { replace: true });
    }
</script>

<main>
    <div class="column">
        <div class="row space-between align-center">
            <span class="text-1">Name:</span>
            {#if editing.name}
                <input
                    type="text"
                    class="text-box"
                    bind:value={userData.name}
                />
            {:else}
                <span class="text-2">{userData.name}</span>
            {/if}
            <div class="row">
                <img
                    src="icon/delete.svg"
                    on:click={() => editable("name", true)}
                    alt="clear"
                />
                <img
                    src="icon/save.svg"
                    on:click={() => editable("name", false)}
                    alt="clear"
                />
            </div>
        </div>
        <div class="row space-between align-center">
            <span class="text-1">Family Name:</span>
            {#if editing.lastname}
                <input
                    type="text"
                    class="text-box"
                    bind:value={userData.lastname}
                />
            {:else}
                <span class="text-2">{userData.lastname}</span>
            {/if}
            <div class="row">
                <img
                    src="icon/delete.svg"
                    on:click={() => editable("lastname", true)}
                    alt="clear"
                />
                <img
                    src="icon/save.svg"
                    on:click={() => editable("lastname", false)}
                    alt="clear"
                />
            </div>
            <!-- <input type="text" class="text-box" bind:value={$user.lastname} /> -->
        </div>
        <div class="row space-between align-center">
            <span class="text-1">ID No:</span>
            {#if editing.idno}
                <input
                    type="number"
                    class="text-box"
                    bind:value={userData.idno}
                />
            {:else}
                <span class="text-2">{userData.idno}</span>
            {/if}
            <div class="row">
                <img
                    src="icon/delete.svg"
                    on:click={() => editable("idno", true)}
                    alt="clear"
                />
                <img
                    src="icon/save.svg"
                    on:click={() => editable("idno", false)}
                    alt="clear"
                />
            </div>
            <!-- <input type="text" class="text-box" bind:value={$user.idno} /> -->
        </div>
        <div class="row space-between align-center">
            <span class="text-1">Birth date:</span>
            {#if editing.birthDate}
                <input
                    type="date"
                    class="text-box"
                    bind:value={userData.birthDate}
                />
            {:else}
                <span class="text-2">{userData.birthDate}</span>
            {/if}
            <div class="row">
                <img
                    src="icon/delete.svg"
                    on:click={() => editable("birthDate", true)}
                    alt="clear"
                />
                <img
                    src="icon/save.svg"
                    on:click={() => editable("birthDate", false)}
                    alt="clear"
                />
            </div>
            <!-- <input type="text" class="text-box" bind:value={$user.birthDate} /> -->
        </div>
        <div class="row space-between align-center">
            <span class="text-1"> Address:</span>
            {#if editing.address}
                <input
                    type="text"
                    class="text-box"
                    bind:value={userData.address}
                />
            {:else}
                <span class="text-2">{userData.address}</span>
            {/if}
            <div class="row">
                <img
                    src="icon/delete.svg"
                    on:click={() => editable("address", true)}
                    alt="clear"
                />
                <img
                    src="icon/save.svg"
                    on:click={() => editable("address", false)}
                    alt="clear"
                />
            </div>

            <!-- <input type="text" class="text-box" bind:value={$user.address} /> -->
        </div>
        <div class="row">
            <span class="text-1">Profile Pic:</span>
            <div class="upload-card">
                <img class="avatar" src={userData.image} alt="upload" />
            </div>
        </div>
        <div class="row justify-end">
            <Link to="/">
                <div class="btn denger" style="margin-right: 10px;">back</div>
            </Link>

            <div class="btn" on:click={editUser}>save</div>
        </div>
    </div>
</main>

<style scoped>
    main {
        margin: 35px 25px 0px 25px;
    }
    .column {
        text-align: left;
        width: 100%;
    }

    .text-box {
        background: #ffffff;
        border: 1px solid #cecece;
        box-sizing: border-box;
        border-radius: 5px;
        width: 100%;
        margin: 0px;
        margin-left: 20px;
    }
    .align-center {
        margin: 0px;
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
