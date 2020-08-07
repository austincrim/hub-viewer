<script>
    export let repo;
</script>

<style>
    .repo {
        transition: transform 0.2s ease-out, box-shadow 0.2s ease-out;
    }
    .repo:hover {
        transform: translateY(-2px);
    }
</style>

<div
    class="flex items-center justify-between p-4 mt-4 bg-gray-200 rounded
    shadow-md hover:shadow-lg repo">
    <span class="text-xl">
        <a
            href={repo.html_url}
            class="hover:text-purple-600 transition-colors duration-75 ease-in">
            {repo.name}
        </a>
    </span>
    <div class="flex space-x-4">
        <div class="flex flex-col items-center">
            <svg
                class="text-gray-800 w-6 h-6"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                viewBox="0 0 24 24"
                stroke="currentColor">
                <path
                    d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1
                    0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1
                    0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538
                    1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976
                    2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0
                    00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1
                    1 0 00.951-.69l1.519-4.674z" />
            </svg>
            <div class="text-lg">{repo.stargazers_count}</div>
        </div>
        <div class="flex flex-col items-center">
            <svg
                class="text-gray-800 w-6 h-6"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                viewBox="0 0 24 24"
                stroke="currentColor">
                <path
                    d="M8.684 13.342C8.886 12.938 9 12.482 9
                    12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0
                    2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0
                    105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368
                    2.684 3 3 0 00-5.368-2.684z" />
            </svg>
            <div class="text-lg">{repo.forks}</div>
        </div>
    </div>

</div>
