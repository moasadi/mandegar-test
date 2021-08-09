<script>
    import { Link, useNavigate } from "svelte-navigator";
    import UploadImage from "../components/uploadImage.svelte";
    const navigate = useNavigate();

    let user = {
        name: "",
        lastname: "",
        idno: "",
        birthDate: "",
        address: "",
        image: "",
        checked: false,
    };
    let submitted = false;

    function saveUser() {
        let users = localStorage.getItem("users");
        users = JSON.parse(users);
        if (!users || users == undefined) {
            users = [];
        }
        users.push(user);
        localStorage.setItem("users", JSON.stringify(users));
        navigate("/", { replace: true });
    }
</script>

<main>
    <div class="column">
        <form
            id="surveyForm"
            class="mt-4"
            class:submitted
            on:submit|preventDefault={saveUser}
        >
            <div class="row space-between align-center">
                <span class="text-1">Name:</span>
                <input
                    type="text"
                    class="text-box"
                    bind:value={user.name}
                    required
                />
            </div>
            <div class="row space-between align-center">
                <span class="text-1">Family Name:</span>
                <input
                    type="text"
                    class="text-box"
                    bind:value={user.lastname}
                    required
                />
            </div>
            <div class="row space-between align-center">
                <span class="text-1">ID No:</span>
                <input
                    type="number"
                    class="text-box"
                    bind:value={user.idno}
                    required
                />
            </div>
            <div class="row space-between align-center">
                <span class="text-1">Birth date:</span>
                <input
                    type="date"
                    class="text-box"
                    bind:value={user.birthDate}
                    required
                />
            </div>
            <div class="row space-between align-center">
                <span class="text-1"> Address:</span>
                <input
                    type="text"
                    class="text-box"
                    bind:value={user.address}
                    required
                />
            </div>
            <div class="row">
                <span class="text-1">Profile Pic:</span>
                <UploadImage bind:user />
            </div>
            <div class="row justify-end">
                <Link to="/">
                    <div class="btn denger" style="margin-right: 10px;">
                        back
                    </div>
                </Link>

                <button class="btn" on:click={() => (submitted = true)}
                    >save</button
                >
            </div>
        </form>
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
</style>
