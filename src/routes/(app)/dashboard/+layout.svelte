<script lang="ts">
    import type { LayoutData } from './$types';
    import { premiumUser } from "$lib/dashboardState";
    import AuthCheck from "$lib/components/AuthCheck.svelte";
    import NavigationBar from "$lib/components/NavigationBar.svelte";
    import { map } from "$lib/mapGen";
    import { user } from "$lib/firebase";
    import { currentAdventure } from '$lib/adventureData';
    import { offScreenMenu } from "$lib/dashboardState";
    import { onMount } from 'svelte';
    import { page } from '$app/stores';
    import LoadingScreen from '$lib/components/LoadingScreen.svelte';
    import { fade } from 'svelte/transition';

    export let data;



    

    let mapArray;
    let mapString;

    map.subscribe(value => {
        mapArray = value;
        mapString = JSON.stringify(mapArray);
    })


</script>


<style>

    .container {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        height: 100vh;
        width: 100%;
   }

    .batlasDashboard {
        display: flex;
        flex: 1;
        flex-direction: row;
        justify-content: flex-start;
        align-items: flex-start;
        width: 100%;
    }

    .batlasDashboard::-webkit-scrollbar {
        display: none;
    }

    .navigation {
        gap: 2rem;
        display: flex;
        position: sticky;
        top: 0rem;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        height: 100%;
        max-height: 100lvh;
        background-color: var(--batlas-black);
    }
    
    .contentSlot {
        height: 100%;
        display: flex;
        flex: 1;
        width: 100%;
        overflow: hidden;
    }


    @media (max-width: 1400px) {
        .container {
            max-height: none;
        }
    }


    @media (max-width: 735px) {

        .container {
            max-height: none;
            overflow: visible;
            height: 100%;
            min-height: 50vh;
        }

        .navigation {
            grid-column: 1 / 2;
            grid-row: 1 / 3;
            margin-top: 0;
            width: 100%;
            max-width: 100%;
            max-height: none;
            position: fixed;
            top: 0rem;
            z-index: 999;
            width: 100%;
            height: auto;
        }

        .contentSlot {
            grid-column: 1 / 2;
            grid-row: 3 / 4;
            margin-top: 0rem;
            max-height: none;
            min-height: auto;
            height: 100%;
            overflow-y: scroll;
            width: 100%;
            max-width: 100%;
            margin-top: 75px;
        }


        .contentSlot {
            padding: 0rem;
            height: 100%;
            max-height: none;
        }
    }
</style>
{#key data.pathname}

<AuthCheck>
    <div class="container" in:fade={{ duration: 300, delay: 400 }} out:fade={{ duration: 300 }}>
        <main class="batlasDashboard">
                {#if $user?.uid === $page.params.creatorId || !$page.url.href.includes('/player/')}
            <section class="navigation">
                <NavigationBar />
            </section>
            {/if}
            <section class="contentSlot noScrollbar">
                <slot />
            </section>
        </main>
    </div>
</AuthCheck>
{/key}
