<script>
    import TailwindStyles from './TailwindStyles.svelte';
    import Repo from './components/Repo.svelte';

    let ghUsername = '';
    let repos = [];

    async function getReposByUser() {
        const res = await fetch(
            `https://api.github.com/users/${ghUsername}/repos`
        );

        if (res.ok) {
            return await res.json();
        }

        throw new Error('User not found');
    }

    function sortRepos(a, b) {
        if (a.stargazers_count > b.stargazers_count) return -1;
        if (a.stargazers_count < b.stargazers_count) return 1;
        return 0;
    }
</script>

<nav>
    <div class="text-3xl text-center py-4 text-purple-100 bg-purple-700">
        Hub Viewer
    </div>
</nav>

<div class="flex flex-col bg-gray-100 min-h-screen py-12">
    <form
        class="flex justify-center space-x-4 py-4"
        autocomplete="off"
        on:submit|preventDefault>
        <input
            id="gh-username"
            placeholder="Github Username"
            bind:value={ghUsername}
            class="px-3 w-1/3 rounded-lg shadow-lg"
            type="text" />

        <button
            id="getReposBtn"
            on:click={() => (repos = getReposByUser())}
            class="px-4 py-2 text-gray-100 bg-purple-600 rounded
            hover:bg-purple-700">
            Get Repos
        </button>
    </form>

    <div class="flex flex-col justify-center items-center">
        {#await repos}
            <p>loading repos...</p>
        {:then repos}
            {#each repos.sort(sortRepos) as repo}
                <div class="w-1/2">
                    <Repo {repo} />
                </div>
            {/each}
        {:catch error}
            <p class="text-red-500">{error.message} :(</p>
        {/await}
    </div>
</div>
