<script lang="ts">
    import {resolveResource, resourceDir} from "@tauri-apps/api/path";
    import {convertFileSrc} from "@tauri-apps/api/tauri";
    import {tauri} from "@tauri-apps/api";

    export let appName: string;

    async function showAPKInFolder()
    {
        const path = (await resourceDir()).substring(4) + "resources\\" +  appName + ".apk";

        await tauri.invoke('show_in_folder', {path});
    }
</script>

<main class="container">
    <h1>{appName}</h1>
    <div class="qrTextHolder">
        <div class="textHolder">
            <p>
                Scan the QR code using your phone to download the APK directly, or alternatively, utilize the button below to locate and manually transfer the APK from your computer to your phone.
            </p>
        </div>
        {#await resolveResource("resources/QR.svg") then qrImage}
            <img class="qr" src={convertFileSrc(qrImage)} alt="">
        {/await}
    </div>
    <button on:click={showAPKInFolder}>Show in folder</button>
</main>

<style>
    .container {
        display: flex;
        flex-direction: column;
        height: calc(100vh - 1.5em);
        justify-content: space-between;
    }

    .qrTextHolder {
        display: flex;
        overflow: hidden;
        flex-grow: 2;
        padding: 0 1.5em;
        justify-content: space-between;
        height: 100%;
    }

    .textHolder {
        display: flex;
        flex-flow: column;
        justify-content: space-between;
        width: 100%;
    }

    h1 {
        text-align: center;
        font-weight: bold;
    }

    p {
        font-size: large;
        margin: 0;
        padding-right: 1em;
    }

    .qr {
        height: min(15em, 45vh);
        align-self: flex-start;
    }

    button {
        border: none;
        /*width: 100%;*/
        width: calc(100vw - 2.5em);
        margin: 0 1.25em;
        padding: 1.75em 0;
        text-align: center;
        text-decoration: none;
        font-size: larger;
        transition-duration: 0.4s;
        cursor: pointer;
        background-color: rgba(114, 137, 218, 0.1);
        border-radius: 5px;
        color: #98aae7;
    }

    button:hover {
        background-color: rgba(114, 137, 218, 0.3);
        color: white;
    }

    * {
        font-family: "Nunito", sans-serif;
        font-weight: normal;
        color: white;
    }

    @font-face {
        font-family: 'Nunito';
        src: url('./fonts/Nunito/Nunito-VariableFont_wght.ttf');
    }
</style>