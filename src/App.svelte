<script>
    import TailwindStyles from "./TailwindStyles.svelte";
    import Repo from "./components/Repo.svelte";

    let ghUsername = "";
    let repos = [];

    async function getReposByUser() {
        const res = await fetch(
            `https://api.github.com/users/${ghUsername}/repos`
        );
        const data = await res.json();
        repos = data;
    }

    window.onload = function() {
        document.querySelector('#gh-username').addEventListener("keyup", (e) => {
            if (e.keyCode === 13) {
                e.preventDefault();
                document.getElementById("getReposBtn").click();
            }
        });
    }
</script>

<div class="flex flex-col bg-gray-100 min-h-screen py-12">
    <div class="flex justify-center space-x-4 py-4">
        <input
            id="gh-username"
            placeholder="Github Username"
            bind:value={ghUsername}
            class="px-3 w-1/3 rounded-lg shadow-lg"
            type="text" />

        <button
            id="getReposBtn"
            on:click={getReposByUser}
            class="px-4 py-2 text-gray-100 bg-purple-600 rounded
            hover:bg-purple-700">
            Get Repos
        </button>
    </div>

    <div class="flex flex-col justify-center items-center">
        {#await repos}
            <p>loading repos...</p>
        {:then repos}
            {#each repos as repo}
                <div class="w-1/2">
                    <Repo {repo} />
                </div>
            {/each}
        {/await}
    </div>
</div>
