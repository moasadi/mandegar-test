<script>
    import { createEventDispatcher } from "svelte";
    import { useNavigate } from "svelte-navigator";


    import { user,indexUser } from "../stores";
    const navigate = useNavigate();

    export let userData;
    export let index;
    const dispatch = createEventDispatcher();
    function handleChange() {
        dispatch("checked", { index, userData });
    }
    function checkItem() {
        $user = userData;
        $indexUser=index;
        navigate("/check", { replace: true });
    }
</script>

<main>
    <div class="mcard">
        <div class="column">
            <div class="column justify-end">
                <input
                    type="checkbox"
                    bind:checked={userData.checked}
                    on:change={handleChange}
                />

                <!-- -->
            </div>
            <div class="row">
                <img
                    src="{userData.image}"
                    class="personal-image"
                    alt="personal"
                />
                <div class="row size">
                    <div class="column margin-10">
                        <span class="text-1">Name</span>
                        <span class="text-1">Family Name</span>
                        <span class="text-1">Birth date</span>
                        <span class="text-1">ID No.</span>
                    </div>
                    <div class="column margin-10">
                        <span class="text-2">{userData.name}</span>
                        <span class="text-2">{userData.lastname}</span>
                        <span class="text-2">{userData.birthDate}</span>
                        <span class="text-2">{userData.idno}</span>
                    </div>
                </div>
            </div>
            <div class="column justify-end">
                <div class="btn" on:click={checkItem}>check</div>
            </div>
        </div>
    </div>
</main>

<style scoped>
    .mcard {
        background: #e3e3e3;
        border: 0.5px solid #c2c0c0;
        box-sizing: border-box;
        border-radius: 5px;
        padding: 5px;
        margin-top: 10px;
        margin-bottom: 10px;
    }
    input {
        margin: 0px;
    }

    .personal-image {
        width: 100px;
        height: 130px;
        object-fit: cover;
        border-radius: 5px;
    }
    .margin-10 {
        margin: 10px;
    }
    .size {
        width: 210px;
    }

    .justify-end {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
    }
</style>
