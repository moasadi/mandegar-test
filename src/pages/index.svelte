<script>
    import { onMount } from "svelte";
    import { Link } from "svelte-navigator";
    import UserCard from "../components/userCard.svelte";

    let users = [];
    let isChecked = false;
    let search = "";
    let selectedAll = false;
    onMount(() => {
        users = JSON.parse(localStorage.getItem("users"));
        if (users) {
            sortUsers();
            findChecked();
        } else {
            users = [];
        }
    });
    function setChecked(e) {
        let data = e.detail;
        users[data.index].checked = data.userData.checked;
        localStorage.setItem("users", JSON.stringify(users));
        sortUsers();
        findChecked();
    }
    function sortUsers() {
        users.sort(function (a, b) {
            return a.checked - b.checked;
        });
        users.reverse();
    }
    function findChecked() {
        const found = users.find((e) => e.checked == true);
        if (found) {
            isChecked = true;
        } else {
            isChecked = false;
        }
    }
    function removeItems() {
        users = JSON.parse(localStorage.getItem("users"));

        var i = 0;
        while (i < users.length) {
            if (users[i].checked === true) {
                users.splice(i, 1);
            } else {
                ++i;
            }
        }
        users = users;
        localStorage.setItem("users", JSON.stringify(users));

        findChecked();
    }

    function selectAndDeselectAll() {
        users.forEach(item=>item.checked=selectedAll)
        users=users;
        localStorage.setItem("users", JSON.stringify(users));

    }
    function searchChange(){
        users = JSON.parse(localStorage.getItem("users"));

         users= users.filter(user => user.name.includes(search))

    }
</script>

<main>
    <div class="column">
        <input
            type="text"
            class="search-box"
            placeholder="search name"
            bind:value={search}
            on:input={searchChange}
        />
        <div class="row space-between">
            {#if isChecked}
                <img
                    src="icon/close_on.svg"
                    on:click={removeItems}
                    alt="close on"
                />
            {:else}
                <img src="icon/close_off.svg" alt="close off" />
            {/if}
            <input
                type="checkbox"
                bind:checked={selectedAll}
                on:change={selectAndDeselectAll}
            />
        </div>
        {#each users as userData, i}
            <UserCard bind:userData index={i} on:checked={setChecked} />
        {/each}
    </div>
    <Link to="add">
        <div class="fab">
            <span>+</span>
        </div>
    </Link>
</main>

<style scoped>
    .search-box {
        background: #ffffff;
        box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.15);
        border-radius: 9px;
        width: 100%;
        height: 48px;
        font-size: 13px;
        background-image: url("/icon/search.svg");
        background-repeat: no-repeat;
        background-position: 10px center;
        padding-left: 35px;
    }
    .fab {
        position: fixed;
        width: 50px;
        height: 50px;
        z-index: 100;
        right: 30px;
        bottom: 30px;
        border-radius: 50%;
        background: #57efdd;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        font-weight: bold;
        color: #fff;
        font-size: 20px;
    }
</style>
