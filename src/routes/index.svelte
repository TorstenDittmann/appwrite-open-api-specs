<script>
    import { onMount } from "svelte";
    import logo from "../logo.svg";

    /** @type {string} */
    let version = '0.10.x';

    /** @type {string} */
    let platform = 'client';

    /** @type {Element} */
    let container;

    /** @type {import('redoc').RedocRawOptions} */
    const config = {
        theme: {
            typography: {
                fontFamily: "Poppins"
            },
            colors: {
                primary: {
                    main: "#f02e65"
                }
            }
        }
    };

    const load = () => {
        Redoc.init(`./specs/${version}.${platform}.json`, config, container);
    }

    onMount(load);
</script>

<svelte:head>
    <title>Appwrite API Specs</title>
</svelte:head>

<header>
    <img src={logo} alt="Appwrite">
    <nav>
        <span class:active={platform === 'client'} on:click={() => (platform = 'client') && load()}>Client</span>
        <span class:active={platform === 'server'} on:click={() => (platform = 'server') && load()}>Server</span>
        <select bind:value={version} on:change={load}>
            <option value="0.10.x">0.10.x</option>
            <option value="0.9.x">0.9.x</option>
            <option value="0.8.x">0.8.x</option>
            <option value="0.7.x">0.7.x</option>
            <option value="0.6.x">0.6.x</option>
        </select>
    </nav>
</header>
<div bind:this={container}></div>


<style>
    :global(body) {
        margin: 0;
        font-family: 'Poppins', sans-serif;
    }

    header {
        height: 4rem;
        display: flex;
        font-size: 1rem;
        align-items: center;
        justify-content: flex-start;
        background-color: #f02e65;
        color: #ffffff;
    }

    header img {
        max-height: 3rem;
        margin-right: 1rem;
    }

    header nav span, header nav select {
        padding: 0 .5rem;
    }

    header nav span {
        cursor: pointer;
    }

    header nav span.active {
        text-decoration: underline;
    }

    header nav span:hover {
        cursor: pointer;
    }

    header nav select {
        font-family: 'Poppins', sans-serif;
        font-size: 1rem;
        background-color: #f02e65;
        color: #ffffff;
        border: none;
    }
</style>