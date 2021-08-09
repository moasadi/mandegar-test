<script>
    let avatar, fileinput;
    export let user = {};
    const onFileSelected = async (e) => {
        let image = e.target.files[0];
        let reader = new FileReader();
        reader.readAsDataURL(image);
        reader.onload = (e) => {
            user.image = e.target.result;
            avatar = e.target.result;
        };
        
    
    };

</script>

<main>
    <div
        class="upload-card"
        on:click={() => {
            fileinput.click();
        }}
    >
        {#if avatar}
            <img class="avatar" src={avatar} alt="d" />
        {:else}
            <img src="/icon/camera.svg" alt="upload" />
        {/if}
        <input
            style="display:none"
            type="file"
            accept=".jpg, .jpeg, .png"
            on:change={(e) => onFileSelected(e)}
            bind:this={fileinput}
        />
    </div>
</main>

<style scoped>
    .upload-card {
        cursor: pointer;
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
