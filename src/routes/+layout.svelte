<script lang="ts">
	import '../app.css';
	import TopNav from '$lib/components/TopNav.svelte';
	import SideNav from '$lib/components/SideNav.svelte';
	import Toast from '$lib/components/Toast.svelte'
	let { children } = $props();
</script>

<Toast/>
<TopNav/>
<div class='w-screen h-16'></div>
<div class="flex flex-grow">
	<SideNav/>
	{@render children()}
</div>

