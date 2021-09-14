<script>
    import { onMount } from 'svelte';
    const { ethers, ContractFactory } = require('ethers');
    import greeter from '../artifacts/contracts/Greeter.sol/Greeter.json';

    let signer;
    let provider;
    let factory;
    let contractAddress = '0xfC50A70935E9b6a6a54854A4c87Cdb346849B7E4';

    onMount(async () => {
        await window.ethereum.enable();
        provider = new ethers.providers.Web3Provider(window.ethereum);
        console.log(provider);
        signer = await provider.getSigner();
        console.log(signer);
        return signer, provider;
    });

    async function mint() {
        console.log(signer);
        // Create an instance of a Contract Factory
        factory = new ContractFactory(greeter.abi, greeter.bytecode, signer);
        // Notice we pass in "Hello World" as the parameter to the constructor
        let contract = await factory.deploy('Hello World');

        contractAddress = contract.address;

        console.log(contract.address);

        console.log(contract.deployTransaction.hash);

        await contract.deployed();
    }

    async function greeting() {
        const greeterContract = new ethers.Contract(
            contractAddress,
            greeter.abi,
            signer
        );
        await greeterContract.greet().then(greeting => {
            console.log(greeting);
        });
    }
</script>

<svelte:head>
    <!-- Primary Meta Tags -->
    <title>SvelteKit ❤️ Tailwind 2</title>
    <meta name="title" content="SvelteKit ❤️ Tailwind 2" />
    <meta
        name="description"
        content="SvelteKit and Tailwind 2 toggle dark/light theme demo"
    />
    <meta
        name="keywords"
        content="Svelte, SvelteKit, Svelte-kit, Tailwind, HTML, CSS, JavaScript"
    />
    <meta name="author" content="@dansvel" />
    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website" />
    <meta property="og:url" content="https://metatags.io/" />
    <meta property="og:title" content="SvelteKit ❤️ Tailwind 2" />
    <meta
        property="og:description"
        content="SvelteKit and Tailwind 2 toggle dark/light theme demo"
    />
    <meta
        property="og:image"
        content="https://sveltekit-tailwind2.netlify.app/screenshot.png"
    />

    <!-- Twitter -->
    <meta property="twitter:card" content="summary_large_image" />
    <meta property="twitter:url" content="https://metatags.io/" />
    <meta property="twitter:title" content="SvelteKit ❤️ Tailwind 2" />
    <meta
        property="twitter:description"
        content="SvelteKit and Tailwind 2 toggle dark/light theme demo"
    />
    <meta
        property="twitter:image"
        content="https://sveltekit-tailwind2.netlify.app/screenshot.png"
    />
</svelte:head>

<main>
    <div
        class="relative min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8 bg-gray-500 bg-no-repeat bg-cover relative items-center"
        style="background-image: url(https://images.unsplash.com/photo-1621243804936-775306a8f2e3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80);"
    >
        <div class="absolute bg-black opacity-60 inset-0 z-0" />
        <div class="sm:max-w-lg w-full p-10 bg-white rounded-xl z-10">
            <div class="text-center mt-4">
                <button
                    on:click={mint}
                    class="block uppercase mx-auto shadow bg-blue-500 hover:bg-indigo-700 focus:shadow-outline focus:outline-none text-white text-xs py-3 px-10 rounded-full"
                    >Mint</button
                >
                <button
                    on:click={greeting}
                    class="block uppercase mx-auto shadow bg-blue-500 hover:bg-indigo-700 focus:shadow-outline focus:outline-none text-white text-xs py-3 px-10 rounded-full"
                    >Greeting</button
                >
                <h2 class="mt-8 text-3xl font-bold text-gray-900">
                    File Upload!
                </h2>
                <p class="mt-2 text-sm text-gray-400">
                    Lorem ipsum is placeholder text.
                </p>
            </div>
            <form class="mt-8 space-y-3" action="#" method="POST">
                <div class="grid grid-cols-1 space-y-2">
                    <label class="text-sm font-bold text-gray-500 tracking-wide"
                        >Title</label
                    >
                    <input
                        class="text-base p-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500"
                        type=""
                        placeholder="mail@gmail.com"
                    />
                </div>
                <div class="grid grid-cols-1 space-y-2">
                    <label class="text-sm font-bold text-gray-500 tracking-wide"
                        >Attach Document</label
                    >
                    <div class="flex items-center justify-center w-full">
                        <label
                            class="flex flex-col rounded-lg border-4 border-dashed w-full h-60 p-10 group text-center"
                        >
                            <div
                                class="h-full w-full text-center flex flex-col items-center justify-center items-center  "
                            >
                                <!---<svg xmlns="http://www.w3.org/2000/svg" class="w-10 h-10 text-blue-400 group-hover:text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
                                    </svg>-->
                                <div
                                    class="flex flex-auto max-h-48 w-2/5 mx-auto -mt-10"
                                >
                                    <img
                                        class="has-mask h-36 object-center"
                                        src="https://img.freepik.com/free-vector/image-upload-concept-landing-page_52683-27130.jpg?size=338&ext=jpg"
                                        alt="freepik image"
                                    />
                                </div>
                                <p class="pointer-none text-gray-500 ">
                                    <span class="text-sm">Drag and drop</span>
                                    files here <br /> or
                                    <a
                                        href=""
                                        id=""
                                        class="text-blue-600 hover:underline"
                                        >select a file</a
                                    > from your computer
                                </p>
                            </div>
                            <input type="file" class="hidden" />
                        </label>
                    </div>
                </div>
                <p class="text-sm text-gray-300">
                    <span>File type: doc,pdf,types of images</span>
                </p>
                <div>
                    <button
                        class="my-5 w-full flex justify-center bg-blue-500 text-gray-100 p-4  rounded-full tracking-wide
                                    font-semibold  focus:outline-none focus:shadow-outline hover:bg-blue-600 shadow-lg cursor-pointer transition ease-in duration-300"
                    >
                        Upload
                    </button>
                </div>
            </form>
        </div>
    </div>
</main>

<style>
    .has-mask {
        position: absolute;
        clip: rect(10px, 150px, 130px, 10px);
    }
</style>
