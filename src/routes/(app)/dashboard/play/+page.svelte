<script>
    import SavedAdventures from "$lib/components/SavedAdventures.svelte";
    import { db, user } from "$lib/firebase";
    import { doc, deleteDoc } from "firebase/firestore";

</script>

<style>

    .fullScreen {
        width: 100%;
        height: 100%;
        }

</style>

<div class="fullScreen">
    <SavedAdventures />
</div>
